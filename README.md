# Test::Fixme [![Build Status](https://secure.travis-ci.org/plicease/Test-Fixme.png)](http://travis-ci.org/plicease/Test-Fixme)

Check code for FIXMEs.

# SYNOPSIS

    # In a test script like 't/test-fixme.t'
    use Test::Fixme;
    run_tests();
    
    # You can also tailor the behaviour.
    use Test::Fixme;
    run_tests( where    => 'lib',      # where to find files to check
               match    => 'TODO',     # what to check for
               skip_all => $ENV{SKIP}  # should all tests be skipped
    );

# DESCRIPTION

When coding it is common to come up against problems that need to be
addressed but that are not a big deal at the moment. What generally
happens is that the coder adds comments like:

    # FIXME - what about windows that are bigger than the screen?

    # FIXME - add checking of user privileges here.

[Test::Fixme](https://metacpan.org/pod/Test::Fixme) allows you to add a test file that ensures that none of
these get forgotten in the module.

# METHODS

## run\_tests

By default run\_tests will search for 'FIXME' in all the files it can
find in the project. You can change these defaults by using 'where' or
'match' as follows:

    run_tests( where => 'lib', # just check the modules.
               match => 'TODO' # look for things that are not done yet.
    );

- where

    Specifies where to search for files.  This can be a scalar containing a
    single directory name, or it can be a list reference containing multiple
    directory names.

- match

    Expression to search for within the files.  This may be a simple
    string, or a qr//-quoted regular expression.  For example:

        match => qr/[T]ODO|[F]IXME|[B]UG/,

- filename\_match

    Expression to filter file names.  This should be a qr//-quoted regular
    expression.  For example:

        match => qr/\.(:pm|pl)$/,

    would only match .pm and .pl files under your specified directory.

- manifest

    Specifies the name of your MANIFEST file which will be used as the list
    of files to test instead of _where_ or _filename\_match_.

        manifest => 'MANIFEST',

# HINTS

If you want to match something other than 'FIXME' then you may find
that the test file itself is being caught. Try doing this:

    run_tests( match => 'TO'.'DO' );

You may also wish to suppress the tests - try this:

    use Test::Fixme;
    run_tests( skip_all => $ENV{SKIP_TEST_FIXME} );

You can only run run\_tests once per file. Please use several test
files if you want to run several different tests.

# SEE ALSO

[Devel::FIXME](https://metacpan.org/pod/Devel::FIXME)

# ACKNOWLEDGMENTS

Dave O'Neill added support for 'filename\_match' and also being able to pass a
list of several directories in the 'where' argument. Many thanks.

# AUTHOR

original author: Edmund von der Burg

current maintainer: Graham Ollis <plicease@cpan.org>

contributors:

Dave O'Neill

gregor herrmann <gregoa@debian.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2014 by Edmund von der Burg <evdb@ecclestoad.co.uk>, Graham Ollis <plicease@cpan.org>.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
