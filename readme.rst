======================================
Chromaprint portable playlist examples
======================================

------------
What this is
------------

This is an extension of the XML Shareable Playlist Format
to include Chromaprint acoustic fingerprints.

It includes an example of a valid XML shareable playlist:

`<chromaprint-playlist.xspf>`_

and a valid JSON shareable playlist:

`<chromaprint-playlist.json>`_

They have no ``location`` field,
but instead a Chromaprint acoustic fingerprint.

----------
Motivation
----------

Electronic playlists are easy to make,
but they aren't as portable as a mix tape on an audio cassette.

This is why the XML Shareable Playlist Format (XSPF) was created.

    One type of shareability is between different pieces of software on the
    same machine. It is common for playlists created with one application to
    not be usable by another application on the same machine, because of
    different or conflicting interpretations of the playlist format. M3U
    suffers from this very badly, because M3U playlists often reference files
    according to a base path which changes from application to application. The
    XSPF group aimed to fix this by providing unambiguous definitions.

    The other type of shareability is between different machines. For playlists
    to be meaningful on different machines, they must be able to identify
    network resources. Audio and video objects are often abstractions like
    "movie X by director Y" rather than computer-friendly objects like
    "whatever file can be gotten from the URI http://foo/x/y". To handle this
    problem, we have provided support for media objects to be found via
    queries; XSPF identifiers are *fuzzy names*.

    [ . . . ]

    XSPF is an intermediate format. We expected a new kind of software called a
    *content resolver* to do the job of converting XSPF to a plain old list of
    files or URIs. A content resolver would be smart enough to keep your
    playlists from breaking when you move your media from /oggs to /music/ogg.
    It would be able to figure out that a playlist entry by the artist "Hank
    Williams" with the title "Your Cheating Heart" could be satisfied by the
    file /vorbis/hankwilliams/yourcheatingheart.ogg. It might even know how to
    query the iTunes music store or another online provider to locate and
    download a missing song.

http://xspf.org/xspf-v1.html

Unfortunately, there is no fully functional content resolver available yet.

Part of the trouble is that quality and consistency of metadata varies wildly,
so resolvers have to guess if a given song is a correct match.

Relying on song length
or a combination of track title, artist, and album
can cause collisions (false matches to the wrong song).

On the other hand, songs have multiple versions
(e.g. re-releases and remasters)
and multiple formats (MP3, OGG, FLAC, AAC, etc.)
so relying on SHA1 hashes or other byte-level checksums
causes the opposite problem (false negatives).

Fortunately, `acoustic fingerprints`_ provide a format-independent identifier,
and the Chromaprint algorithm has an open-source implementation
which is in widespread use by the MusicBrainz/AcoustID project.

https://acoustid.org/chromaprint

A Chromaprint is a list of signed 32-bit integers
(encoded as Base64 to save characters).
so determining if a song is the same (or close enough)
becomes much easier.

https://oxygene.sk/2011/01/how-does-chromaprint-work/

.. _acoustic fingerprints: https://en.wikipedia.org/wiki/Acoustic_fingerprint

---------------------
What needs to be done
---------------------

I don't know of any music player that accepts this format.

Once there is a player that indexes its songs by Chromaprint
and can play them back
based on similarity to the list of Chromaprints in the playlist,
this format will be much more useful.
