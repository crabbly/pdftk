* 2.02 - July 24, 2013
  * Added drop_xmp output option for removing the document XMP metadata
            stream from a PDF.
  * Added dump_data output of custom page data embedded by STAMPtk
            tool. See the embed option in STAMPtk for more information.
  * Improved PDF bookmark merging logic so it can handle more input
            cases.
  * Fixed a password bug where some 'upper-ASCII' characters weren't
            being mapped to the correct code points.
  * Fixed a 40-bit decryption bug introduced in version 2.00.
  * Fixed a bug in the bookmark merging logic that caused bookmarks to
            be omitted from the merged PDF.
  * Added a test to ensure that encryption passwords use permitted
            characters only. (Decryption attempts still allow a larger set of
            input characters.)
  * Rewrote the wide-to-utf8 code for Windows to make it more rigorous.
  * Organized our calls of JvInitClass() in main().
  * Added descriptions to some exception reports.
  * Reviewed some code from pdftk.cc, PdfReader.java, PdfWriter.java
            and friends.
* 2.01 - June 5, 2013
  * Fixed an uncompress bug introduced in 2.00 that corrupted some
            image streams.
  * Updated the Windows pdftk.exe compiler settings to remedy an
            elusive NullPointerException reported in the field. This problem
            first appeared in version 2.00.
* 2.00 - May 22, 2013
  * Added AES decryption of input PDFs. The 'owner' password is still
            required when decrypting any PDF.
  * Added merging of bookmarks/outlines when merging full PDFs.
  * Added new rotate operation, which is a convenient way of rotating
            select pages of a single PDF.
  * Added new dump_data_annots operation. Currently it reports only
            link annotation information.
  * Added new need_appearances output option. Use this when filling a
            form with non-ASCII text to ensure the best presentation in Adobe
            Reader/Acrobat. It won't work when combined with the flatten
            option.
  * Improved the compress option so that output PDFs are more compact
            and efficient.
  * Added page media information to dump_data output: page rotation,
            page media bounds and page crop bounds.
  * Improved the performance of dump_data so it works better with very
            large PDFs.
  * Improved the memory management in the Windows binary. This fixes
            the rare "Too many heap sections" error.
  * Fixed a bug where form fields with multiple values were not being
            properly reported by dump_data_fields.
  * Fixed a_burst_bug that was corrupting the output PDF pages.
  * Fixed an_input_bug to allow interactive prompting of both the user
            and owner passwords.
  * Fixed a burst bug so that doc_data.txt is now output to the same
            directory as the PDF's pages when an output directory is given.
  * Fixed a bug where indirect references to the PDF ID in the trailer
            would cause a crash.
  * Added a test to fill_form so it checks that an input PDF is a form
            before trying to fill it with data.
  * Added a return value of 3 for warnings 'PDF information not added'
            or 'PDF form not filled.'
  * Improved the error message for cat page range errors.
  * Fixed the error report when an input page number is out of range.
  * Fixed a burst bug where document metadata wasn't being copied
            properly to the output PDFs.
  * Updated the Bouncy Castle library to 1.48.
  * When using the cat operation, the output PDF version number is now
            set to the maximum PDF version of all of the input PDFs. If any of
            the input PDFs have PDF extension levels, then the greatest
            extension level is also copied to the output PDF.
* 1.45 - December 6, 2012
  * You can now add or change a PDF's bookmarks using update_info.
  * Added record delimiters to dump_data output to help make parsing
            more reliable.
  * The changes to dump_data output (described above) are also now
            required for the input to update_info.
  * You can now use multi-character input handles. Prior versions were
            limited to a single character, imposing an arbitrary limitation on
            the number of input PDFs when using handles. Handles still must be
            all upper-case ASCII.
  * Added means of referring to PDF pages in reverse order. By
            prefixing a page number with an r, it counts from the end of the
            document. For example, r1 is the last page, r2 is the next-to-last
            page, etc.
  * Changed the syntax for page rotation. Instead of N, S, E, W, L, R
            and D, now use: north, south, east, west, left, right and down.
  * Fixed a problem reading input PDF filenames that have non-ASCII
            characters on Windows 7.
  * Fixed a stream parsing issue with troublesome PDFs that don't
            strictly follow the PDF specification.
* 1.44 - October 28, 2010
  * Added new feature for collating PDF page scans: shuffle. Please see
            the man page for usage details.
  * Introduced update_info_utf8, dump_data_utf8 and
            dump_data_fields_utf8 to provide UTF-8 companions to update_info,
            dump_data and dump_data_fields. These latter operations use XML
            numerical entities to encode non-ASCII characters. In version 1.43,
            we changed the encoding for update_info to UTF-8, but that made it
            incompatible with dump_data and also broke some downstream
            applications. By introducing these UTF-8 operations, we can revert
            update_info to its original behavior.
  * Burst feature now copies the metadata (including XMP) from the
            input file to the output pages.
  * Updated Bouncy Castle library to 1.45.
  * Removed or replaced third-party code that wasn't compatible with
            pdftk's GPL license.
  * Updated third-party license information.
* 1.43 - September 30, 2010
  * Improved input handle detection to reduce false hits.
  * Improved keyword detection logic to eliminate false hits when input
            filenames happen to include pdftk keywords even, odd and end.
  * Added option of prompting the user for the output when bursting a
            PDF. Also reviewed other filename prompting code.
  * Changed the PDF parser to accept name tokens longer than 127
            characters -- the PDF Specification says that 127 is the limit.
            This isn't related to file names. The issue arose with PDFs created
            by Acrobat Web Capture 9.0.
  * Fixed a problem with filling form choice fields in some PDFs where
            the old form value was 'sticking.'
  * Changed pdftk behavior when handling subset fonts so it doesn't
            alter font name "tags." This was causing printing problems with
            Acrobat 3.01 on Windows.
  * Fixed a stream parsing bug that was causing page content to
            disappear after merge of PDFs generated by Microsoft Reporting
            Services PDF Rendering Extension 10.0.0.0.
  * Added multistamp and multibackground features provided by a Debian
            patch -- thanks!
  * Clear the signal mask as workaround to environments that turn off
            signals before calling pdftk. This problem is known to cause pdftk
            to hang_in_some_Python_web_setups as well as in PHP.
  * Set locale to C as workaround to an unusual exception. This is a
            Debian_patch. Please let me know if it causes any troubles.
  * Improved reporting of output errors via Debian patch -- thanks!
  * Added support for UTF-8 data in update_info via Debian patch -
            - thanks!
  * Added support for UTF-8 filenames via Debian patch -- thanks!
  * Updated build procedure to work better with newer versions of GCC.
            Maintained compatibility with older versions of GCC.
  * Added license information to the source tree for the third-party
            libraries that pdftk uses.
* 1.41 - November 28, 2006
  * Fixed a bug that corrupted output PDF xref tables. This corruption
            was mild but universal. Most PDF tools can cope with the corrupted
            PDFs, but I recommend upgrading from 1.40 to 1.41 as soon as
            possible. This bug was introduced in version 1.40 -- version 1.12
            does not have this bug.
  * Fixed a bug that prevented XFDF form data from being passed to
            pdftk via stdin.
  * Commented out some unused code from pdftk.cc.
* 1.40 - September 19, 2006
  * Added the stamp operation, a natural complement to the existing
            background operation.
  * Added the page rotating patch provided by David Fabel -- thanks!
            Tweaked the patch so it handles a greater variety of input syntax
            (e.g., 1-20evenE).
  * Added the generate_fdf patch provided Bernhard R. Link -- thanks! I
            actually rewrote the patch so it uses FDF features built into the
            iText library. Please let me know my changes break anything
            downstream.
  * The fill_form operation can now take XFDF data as well as FDF data.
            This feature was sponsored by Vesaria -- thanks!
  * Added the drop_xfa option so pdftk could fill forms created with
            newer versions of Acrobat or Adobe Designer. Read more about this
            above.
  * Added the keep_first_id and keep_final_id options for more PDF fun.
  * Upgraded the iText library we use to itext-paulo rev. 155. This
            makes pdftk harder to compile on older versions of gcc.
  * Added the -O2 optimizing switch to Makefile GCJFLAGS. This should
            make pdftk leaner and meaner, but could be dropped if your build
            acts funny (like segfaulting).
  * Fixed a bug that caused pdftk to create bloated PDFs when input PDF
            pages had links on their pages.
  * Added License-Adobe.txt to the fonts folder, as required for
            distribution of Adobe's AFM files.
* 1.12 - November 9, 2004
  * Fixed a bug where the presense of page annotations in some PDFs
            would cause pdftk to crash. This bug first emerged when processing
            a PDF created by FPDF (version 1.52) that contained web links.
            Turns out that pdftk erroneously expected all page annotations to
            be indirect objects. This assumption has been removed from the
            code.
* 1.11 - November 3, 2004
  * Fixed a couple bugs in the dump_data_fields form field reporting.
            Also improved this feature so it now reports all possible settings
            for check box, radio button, list box and combo box form fields.
* 1.10 - October 27, 2004
  * Fixed the background feature so it handles rotated pages (input PDF
            or background PDF) better. Pdftk will transform the background PDF
            page so that its orientation is preserved on every page of the
            output PDF, even on input PDF pages that are rotated. I chose this
            logic so as to give the user greater control over the results;
            rotate pages before processing to achieve the desired output. Let
            me know if this logic is too inconveniet for you.
  * Fixed form field handling when combining PDF pages. Pdftk used to
            permit duplicate form field names, which is illegal PDF. Now, pdftk
            detects duplicates and adds name prefixes as needed. If no
            duplicates occur, then no changes are made. If an input PDF has a
            field represented by multiple annotations, then that is respected
            and preserved in the output.
            An especially nice upshot to this new handling is that you can now
            assemble duplicate PDF forms and not end up with all of their
            fields echoing each other (as you get with Acrobat). Run pdftk
            A=form.pdf cat A A A output formX3.pdf and you'll get a form that
            behaves as you would expect.
  * Added stdin support for input PDF, FDF, or Info files (thanks to
            Bart Orbons for this patch).
  * Added a means for users to control the output PDF filenames when
            using the burst feature: pass in a printf-styled format string via
            output (documented above).
  * Changed background command-line syntax, so it is an operation
            instead of an output option. The old syntax also works, for
            backward compatibility.
  * Now shuffling subset font name prefixes for input PDFs, to prevent
            duplicates.
  * Updated Makefile.Mandrake according to feedback from Larry
            Gilliland.
  * Reduced the Windows EXE filesize using UPX, as suggested by Ralf
            Koenig.
* 1.00 - August 14, 2004
  * Upgraded the iText library we use to itext-paulo rev. 132, which
            resolved a bug involving bookmark page references in dump_data
            output.
  * Fixed the problem of form fields getting corrupted by splitting or
            merging PDF form pages.
  * Building the Windows binary using libgcj 3.4 seems to have fixed
            the problem of using accented characters in filenames and paths.
  * Added these new operations: fill_form, update_info, attach_file,
            and unpack_file.
  * Added the background and flatten output options.
  * Added the do_ask interactive mode (the default on Windows) that
            asks before overwriting files and asks for passwords to input PDFs,
            if necessary. Also added the dont_ask mode (the default on Linux),
            for hands-free operation.
  * Many input fields can be substituted with PROMPT, which cues pdftk
            to ask the user for a filename or password upon execution.
  * Added output to stdout via output -.
  * Using the uncompress option now also adds page numbers to page
            dictionaries, for easy lookup. Find page N (1-based) by searching
            for /pdftk_PageNum N. Using the compress option removes these
            markers.
  * Added Mac OS X Makefile, and removed the optimization flag from the
            GCJ flags (which would cause trouble on older versions of gcc, such
            as 3.2.2) in all Makefiles.
  * Now catching PDF output open exceptions.
  * Builds now pack iText font afm files into pdftk, which are required
            for the new form filling feature.
* 0.941 - March 28, 2004
  * Fixed the 'Input_UnicodeBig not found' error encountered by Windows
            users when using the dump_data or the burst operations on some
            PDFs.
  * Added an optimization flag to the gcj arguments. This can be
            adjusted or omitted by editing your platform-specific Makefile.
  * Renamed the CC_OPTS Makefile macro to CXXFLAGS, for uniformity.
* 0.94 - March 24, 2004
  * Fixed a string copy bug in pdftk.cc.
  * Fixed unicode string output so it drops initial, signature
            character.
  * Fixed nagging gnu.java.locale.Calendar static linking problem
            (Windows).
  * Made more improvements towards gcc/gcj 3.2 compatibility (e.g.,
            RedHat 8, 9).
  * Added macros to Makefiles, for easier porting.
  * Added simple return codes: 0 --> Success, 1 --> Error, 2 --
            > Exception. Some exceptions will return an "Error" return code.
  * Removed warning issued when an input PDF has no ID string.
  * Empty Info fields no longer reported on dump_data.
  * Added newline to end of --help output.
* 0.93 - March 7, 2004
  * Removed restriction on the number of input documents. For example,
            you can now run:
            pdftk *.pdf cat output combined.pdf
            to assemble any number of PDFs into a single document.
  * Made pdftk run silently by default, and added the verbose output
            option for when you want detailed feedback.
  * Changed the encryption strength default from 40-bit to 128-bit.
  * Improved file open error handling and reporting. If pdftk can't
            open a PDF, it tells you why.
  * Added RedHat9 and Mandrake makefiles (Thanks to Andre Gompel and
            Pablo Rodri'guez). Support for these platforms is still
            experimental.
  * Copied the MD5 code from libgcj into our tree, to improve support
            for older compilers/libraries. This should improve RedHat9 and
            Mandrake support.
  * Removed pointless warning sometimes issued by the libgcj security
            class.
  * Added debian directory and Aure'lien's man page, updated man page.
  * Reorganized Makefiles (thanks Andre).
* 0.92
  * Added logical page numbering (a/k/a page labels) to dump_data
            operation.
  * Appended .omit extension to a few iText files we don't use, to
            speed compiling.
* 0.91
  * Removed restriction on adding the same page from the same PDF more
            than once.
  * Added Solaris Makefile.
  * AllFeatures permission now implies 'top quality' printing, not
            'degraded' printing.
  * Fixed handling of 'empty owner password' case during output
            encryption.
  * Added test to make sure the user password is not the same as the
            owner pw.
  * CopyContents also allows ScreenReaders.
  * ModifyAnnotation also sets the FillIn bit.
  * ModifyContents also sets the Assembly bit.
  * Updated docs.
  * Added --version switch.
