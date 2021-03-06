# dumppoppy

Usage: dumppoppy [options] destname sourcefile

Parses through content of the sourcefile, finding each e-mail
retrieved via a "RETR ###" POP3 command, writing each to the file:
mail.destname.###, where ### is the number RETRieved.

If identical messages are retrieved, a checksum may be used to
eliminate duplicates. On non-Windows boxes where Digest::MD5 can be
found, this is done automatically (unless -U is used).

If Digest::MD5 cannot be found, or if dumppoppy is run from a Windows
host, a simple and slow checksum CAN BE used by adding the additional
-U option. This simple checksum is not 100% reliable, and it may happen
that different messages are mistakenly identified as duplicates.

Unless the -c (clobber) option is used, if two RETR commands of the
same ### result in different messages, both will be preserved, with
each subsequent RETR of the same ### named "mail.destname.###.MMM",
where MMM is the first, starting at 000, that does not yet exist. This
may happen if two different users' mail are in the file being parsed,
and both happen to have the same ### message with different content.

OUTPUT: dumppoppy will print to STDOUT one or more informational
        messages per RETRieved mail found (unless -q is used).


OPTIONS

-d dir  Destination directory in which to write files. DEFAULT: ./
-c      FORCE clobber of multiple RETR commands of the same message.
        Only useful if multiple RETR of the same number WILL DEFINITELY
        be from the same user AND resulted in different content (maybe
        one was partial). MD5 sum will take care of identical RETRieved
        messages nicely, so -c should seldom be needed.
-q      Quiet--only show error output
-A      DO NOT assume that "^Connection closed by foreign host" is the
        end of a message. DEFAULT DOES.
-U      Toggle de-dupe. (see above)

Usage: dumppoppy [options] destname sourcefile

dumppoppy version 1.0.1.2
