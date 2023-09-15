This is a fork of Mattias Kettner's mk_livestatus. It has been ported to
Nagios 4 and contains some extra features such as sorting and page offsets.
This branch is being maintained by op5 until such a time comes when everything
we need has been merged back upstream.

To find out more about mk_livestatus, see
 http://mathias-kettner.de/checkmk_livestatus.html

=== Differences between mk_livestatus and op5 fork of livestatus ===

Three additions to Livesetatus Query Language is added:

-----
Sort: <column name> <asc/desc>

Sorts the result set by the specified column in the given direction. Multiple
Sort lines can be added. First sort line takes precedance.

Example:

GET hosts
Sort: last_hard_state_change desc

-----
Offset: <number of lines>

Lines to skip from the beginning of the result set. Useful for pagination in
combination with Limit header.

Example:

GET services
Sort: host_name asc
Sort: description asc
Limit: 100
Offset: 300

-----
OutputFormat: wrapped_json

An extension to the json output format.
The result set is packed in a json object, with a couple of possible fields:
- columns: an array of column names. (optional)
- data: an array of arrays, describing the result set, in the same syntax common
  json output, without embedded column names.
- total_count: The number of lines in the resultsed, except the limitation of
  Limit and Offset headers.

=== About op5 ===

To find out more about op5, see
 http://op5.org

=== INSTALL ===

To install, run (as a root):
 autoreconf -s
 automake --add-missing
 ./configure CPPFLAGS=-I./nagios/
 make
 make install
