# Table of Contents

1. [description](#description)

2. [data-format](#data-format)

3. [batch-training](#batch-training)


# description

Package:      areas/neural/systems/cascor/

Name:         CASCOR

Summary:      Lisp and C implementations of Cascade Correlation

Version:      C 1.1 (31-MAY-94); Lisp 1.0 ()

Description:

   This directory contains C and Lisp implementations of the Cascade
   Correlation Algorithm.

   The Lisp code was written by Scott Fahlman, then ported to C by
   Scott Crowder. More recent C versions have been re-engineered by Matt
   White.  Features have been added to allow data sets from the CMU
   learning benchmark database to run on this system.

Requires:     C, Lisp

Ports:

Origin:       ftp.cs.cmu.edu:/afs/cs.cmu.edu/project/connect/code/
              as the files cascor-v1.1.shar and cascor1.lisp
              and in /afs/cs.cmu.edu/project/connect/tr/ as cascor-tr.ps.Z

Copying:      Public Domain

Updated:      Thu Sep  1 19:18:52 1994

CD-ROM:       Prime Time Freeware for AI, Issue 1-1

Bug Reports:  neural-bench@cs.cmu.edu

Mailing List:

Author(s):    Scott Fahlman <sef+@cs.cmu.edu>
              R. Scott Crowder <crowders@tcplink.nrel.gov>
              Matt White <mwhite+@cmu.edu>

Contact:      neural-bench@cs.cmu.edu

Keywords:

   Neural Networks, Cascade Correlation, C!Code, Lisp!Code, CMU,
   Public Domain, Authors!Fahlman, Authors!Crowder, Authors!White,
   Machine Learning!Neural Networks, CASCOR

Contains:    ???

See Also:

   areas/neural/bench/

References:

   Scott E. Fahlman and Christian Lebiere, "The Cascade-Correlation
   Learning Architecture", in D. S. Touretzky, editor, "Advances in
   Neural Information Processing Systems 2", Morgan Kaufmann, 1990.  A
   somewhat longer version is available as CMU Computer Science Tech
   Report CMU-CS-90-100, a copy of which is included in the distribution.

   Marcus Hoehfeld and Scott E. Fahlman (1992) "Learning with Limited
   Numerical Precision Using the Cascade-Correlation Learning Algorithm"
   in IEEE Transactions on Neural Networks, Vol. 3, no. 4, July 1992, pp.
   602-611.


# data-format

CMU Neural Network Learning Benchmark Database
Data File Format

Maintainer:  neural-bench@cs.cmu.edu

  This file contains a description of the standard format for data files in the
CMU learning benchmark collection.  These files are a supplement to the
benchmark description files that comprise the CMU Benchmark Collection.  Data
files are associated to their appropriate description file with a '.data'
extension to the file name of the benchmark description.


  SEGMENTS
  --------
  Each data set is composed of two to four segments.  The first segment
is always the $SETUP segment.  The $SETUP segment is immediately followed by
the $TRAIN segment.  There are also optional $VALIDATION and $TEST segments.

  $SETUP
  ======
    The $SETUP segment describes the requirements of the network to the
  program.  Included in this segment is information on how the program should
  read the actual data segments as well as what type of inputs and outputs are
  required.  All lines in the $SETUP segment should end in a ';'.

    PROTOCOL: {IO, SEQUENCE};
      The protocol parameter tells the program how to read the data sets
    included in the file.  In an IO mapping, each vector of input and output
    values is a seperate training case, independant of all others.  The
    network's output depends only on the current inputs.  In a SEQUENCE
    mapping, the input/output vectors are presented in sequential order.  The
    output may depend on earlier inputs as well as the current input vector.

    OFFSET: <n>;
      This appears only in SEQUENCE mappings.  It is the number of input
    vectors to read before an output should be produced.  For most problems,
    this will be set to '0'.

    INPUTS: <n>;
      This is the number of items in an input vector.  However, since some
    data types, such as enumerations, may require more than one input unit to
    represent, the actual number of input units may be greater.

    OUTPUTS: <n>;
      Similar to INPUTS, this specifies outputs instead of inputs.  Again,
    due to some data types requiring more than one unit to represent, there
    may be a disparity between this number and the actual number of output
    nodes in the network.

    IN [n]: < CONT {Domain}, BINARY, ENUM {list} >;
      Each input must have an explicit entry describing it.  This entry
    contains the node number (n) and a data type.  Available types are:
    CONTinuous, BINARY, and ENUMerated.  Continuous inputs are floating
    point numbers with a specified domain (where all numbers are guaranteed to
    fall).  Binary inputs have either a value of '+' or '-'.  An enumerated
    input is one of a list specified within '{}'.

    OUT [n]: < CONT {CoDomain}, BINARY, ENUM {list} >;
      Each output must also have an explicit entry describing it.  This entry
    contains the node number (n) and a data type.  A CONT output is a
    floating point output which is guaranteed to fall within a specified
    CoDomain.  BINARY outputs should have either a positive, '+', or a
    negative, '-', value.  An ENUMerated output is one of the specified list.

    NOTE -  While listing node types, no fields are acceptable.  In other
    words, the definition 'IN [1..13]: BINARY' or 'OUT [1]: ENUM {A..Z}'
    would NOT be legal.


  $TRAIN, $VALIDATION, $TEST
  --------------------------
    These segments contain the actual training, validation and testing data to
  be used by the network.  The validation and testing segments are optional.
  Entries into one of these segments should have the form:

	<input 1>, <input 2>, <etc>  =>  <output 1>, <output 2>, <etc>;

    In SEQUENCE data sets, there may also be '<>' delimiters.  These specify
  the end of a sub-sequence.  Data sets on opposite sides of one of these
  delimiters should not affect eachother.  The sequence-end delimiters do NOT
  require a semicolon, as do not segment headers.
    In data sets with an offset, there should be no arrow and no outputs for
  the first (n) inputs.  Simply end the list of inputs with a semicolon.


  COMMENTS
  --------
    While no actual comment card is specified, any text occuring on a line
  after a semicolon should NOT be parsed.  Therefore it is possible to
  comment a data file by starting a line with a semicolon.


# batch-training

From sef@sef-pmax.slisp.cs.cmu.edu Wed Mar  2 18:52:51 EST 1994
Article: 14911 of comp.ai.neural-nets
Xref: glinda.oz.cs.cmu.edu comp.ai.neural-nets:14911
Newsgroups: comp.ai.neural-nets
Path: honeydew.srv.cs.cmu.edu!news
From: sef@sef-pmax.slisp.cs.cmu.edu
Subject: Re: online cascade-correlation
Message-ID: <CLMvwu.1Ku.3@cs.cmu.edu>
Sender: news@cs.cmu.edu (Usenet News System)
Nntp-Posting-Host: sef-pmax.slisp.cs.cmu.edu
Organization: School of Computer Science, Carnegie Mellon
Date: Tue, 22 Feb 1994 16:17:17 GMT
Lines: 47


    From: B35@vm.urz.uni-heidelberg.de (Matthijs Kadijk)

    In a recent posting by Scott E. Fahlman, he wrote that some people
    have addapted cascor for online (i.s.o. batch) learning. I would be
    interested to try this out the learning problem I'm corrently working
    on.

I don't have code for this, but what you need to do is the following:

1. Replace the quickprop weight update with simple gradient descent, with
or without momentum according to taste.

2. Rip out the cacheing mechanism, since it no longer makes sense to cache
the network's results for a whole epoch.

3. Modify the quiescence tests to keep some kind of running average and to
stop when there is no net improvement for a long time.  Note that in online
updating, the error or correlation score does not smoothly approach an
asymptote, but continues to bounce around as new samples arrive.

4. Optional: In the online case, it may be desirable to run output and
candidate training concurrently.  Just make sure that candidate training
continues for some time after the output weights have finally been frozen.

5. If you are running the net for performance and training at the same
time, introduce new hidden units with a very small initial output weight
(of the proper sign) so that you don't create too much of a bump in the
network's performance.

By the way, I have seen a few claims that Cascor runs better if Quickprop
is replaced by simple gradient descent, even in the batch-training case.  I
don't believe these claims, and that has not been my experience.  I will
admit that it can be a bit tricky to adjust the epsilon parameter in
Quickprop to get best performance, however.

-- Scott

===========================================================================
Scott E. Fahlman			Internet:  sef+@cs.cmu.edu
Senior Research Scientist		Phone:     412 268-2575
School of Computer Science              Fax:       412 681-5739
Carnegie Mellon University		Latitude:  40:26:33 N
5000 Forbes Avenue			Longitude: 79:56:48 W
Pittsburgh, PA 15213
===========================================================================
