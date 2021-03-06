```
usage: swappxdata [options] <file>|<directory>...

The swappxdata utility swaps bytes of uncompressed pixel data with Value
Representation OW. For each successfully updated file a dot (.) character
is written to stdout. For each file kept untouched, one of the characters:
p - no pixel data)
c - compressed pixel data)
b - pixel data with Value Representation OB)
l - little endian encoded pixel data)
8 - pixel data with 8 bits allocated)
is written to stdout. If an error occurs on updating a file, an E
character is written to stdout and a stack trace is written to stderr.
-
Options:
 -h,--help              display this help and exit
    --if-big-endian     test encoding of pixel data; keep files untouched,
                        if the pixel data is encoded with little endian or
                        8 bits allocated. By default, bytes of
                        uncompressed pixel data with Value Representation
                        OW will be swapped, independent of its encoding.
    --log <pattern>     specifies which attributes of updated objects are
                        logged. '{ggggeeee}' will be replaced by the
                        attribute value. By default, no log file is
                        written.
    --log-file <path>   path of file to which attributes of updated
                        objects are logged. './uids.log' by default.
    --test-all          test encoding of pixel data of each file. By
                        default, if one file of a directory is detected as
                        not big endian encoded, all remaining files of the
                        directory are kept also untouched without loading
                        them in memory for testing.
    --uids              log SOP Instance UIDs from updated files in log
                        file, equivalent with --log={00080018}.
 -V,--version           output version information and exit
-
Example: swappxdata --if-big-endian --log
'{0020000D};{0020000E};{00080018}' storage/2020/09/
=> Swaps bytes of big endian encoded pixel data in DICOM files in
directory storage/2020/09/ and logs the Study Instance UID (0020,000D},
Series Instance UID (0020,000E) and SOP Instance UID (0008,0018) of
updated objects separated by semicolons to ./uids.log.
```