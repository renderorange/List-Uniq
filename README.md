# NAME

List::Uniq - extract the unique elements of a list

# SYNOPSIS

    use List::Uniq ':all';

    @uniq = uniq(@list);

    $list = [ qw|foo bar baz foo| ];
    $uniq = uniq($list);

# DESCRIPTION

List::Uniq extracts the unique elements of a list.  This is a commonly
re-written (or at least re-looked-up) idiom in Perl programs.

# FUNCTIONS

## uniq( { OPTIONS }, ele1, ele2, ..., eleN )

uniq() takes a list of elements and returns the unique elements of the list. 
Each element may be a scalar value or a reference to a list.

If the first element is a hash reference it is taken to be a set of options
that alter the way in which the unique filter is applied.  The keys of the
option set are:

- sort

    If set to a true value, the unique elements of the list will be returned
    sorted.  Perl's default sort will be used unless the **compare** option is
    also passed.

    **sort** defaults to false.

- flatten

    If set to a true value, array references in the list will be recursively
    flattened, such that

        ( 'foo', [ [ 'bar' ] ], [ [ [ 'baz', 'quux' ] ] ] )

    becomes

        ( 'foo', 'bar', 'baz', 'quux' )

    **flatten** defaults to true.

- compare

    A code reference that will be used to sort the elements of the list if the
    **sort** option is set.  Passing a non-coderef will cause **uniq** to throw an
    exception.

    The code ref will be passed a pair of list elements to be compared and
    should return the same values as the [cmp](https://metacpan.org/pod/perlop#Equality-Operators)
    operator.

    Using a custom sort slows things down because the sort routine will be
    outside of the List::Uniq package.  This requires that the pairs to be
    compared be passed as parameters to the sort routine, not set as package
    globals (see ["sort" in perlfunc](https://metacpan.org/pod/perlfunc#sort)).  If speed is a concern, you are better off
    sorting the return of **uniq** yourself.

The return value is a list of the unique elements if called in list context
or a reference to a list of unique elements if called in scalar context.

# EXPORTS

Nothing by default.

Optionally the **uniq** function.

Everything with the **:all** tag.

# SEE ALSO

- [Array::Unique](https://metacpan.org/pod/Array%3A%3AUnique)

    If you want to unique a list as you insert into it, see [Array::Unique](https://metacpan.org/pod/Array%3A%3AUnique).

- ["uniq" in List::Util](https://metacpan.org/pod/List%3A%3AUtil#uniq)
- ["uniq" in PerlPowerTools](https://metacpan.org/pod/PerlPowerTools#uniq)

# AUTHOR

James FitzGibbon
&lt;james+perl@nadt.net>

# CREDITS

The idioms used to unique lists are taken from recipe 4.7 in the _Perl
Cookbook, 2e._, published by O'Reilly and Associates and from the Perl FAQ
section 5.4.

I pretty much just glued it together in a way that I find easy to use. 
Hopefully you do too.

# COPYRIGHT

Copyright (c) 2004-2008 Primus Telecommunications Canada Inc.

Copyright (c) 2008-2010 James FitzGibbon

All Rights Reserved.

This library is free software; you may use it under the same
terms as perl itself.
