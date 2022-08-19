**Important:** Read CONTRIBUTING.md before submitting feedback or contributing
```




dnsop                                                          W. Kumari
Internet-Draft                                                    Google
Intended status: Informational                                P. Hoffman
Expires: 20 February 2023                                          ICANN
                                                          19 August 2022


                  The ALT Special Use Top Level Domain
                      draft-ietf-dnsop-alt-tld-16

Abstract

   This document reserves a TLD label, "alt" to be used in non-DNS
   contexts.  It also provides advice and guidance to developers
   developing alternative namespaces.

   [ This document is being collaborated on in Github at:
   https://github.com/wkumari/draft-wkumari-dnsop-alt-tld.  The most
   recent version of the document, open issues, etc should all be
   available here.  The authors (gratefully) accept pull requests. ]

Status of This Memo

   This Internet-Draft is submitted in full conformance with the
   provisions of BCP 78 and BCP 79.

   Internet-Drafts are working documents of the Internet Engineering
   Task Force (IETF).  Note that other groups may also distribute
   working documents as Internet-Drafts.  The list of current Internet-
   Drafts is at https://datatracker.ietf.org/drafts/current/.

   Internet-Drafts are draft documents valid for a maximum of six months
   and may be updated, replaced, or obsoleted by other documents at any
   time.  It is inappropriate to use Internet-Drafts as reference
   material or to cite them other than as "work in progress."

   This Internet-Draft will expire on 20 February 2023.

Copyright Notice

   Copyright (c) 2022 IETF Trust and the persons identified as the
   document authors.  All rights reserved.

   This document is subject to BCP 78 and the IETF Trust's Legal
   Provisions Relating to IETF Documents (https://trustee.ietf.org/
   license-info) in effect on the date of publication of this document.
   Please review these documents carefully, as they describe your rights
   and restrictions with respect to this document.  Code Components



Kumari & Hoffman        Expires 20 February 2023                [Page 1]

Internet-Draft               Reserve ALT TLD                 August 2022


   extracted from this document must include Simplified BSD License text
   as described in Section 4.e of the Trust Legal Provisions and are
   provided without warranty as described in the Simplified BSD License.

Table of Contents

   1.  Introduction  . . . . . . . . . . . . . . . . . . . . . . . .   2
     1.1.  Requirements Notation . . . . . . . . . . . . . . . . . .   2
     1.2.  Terminology . . . . . . . . . . . . . . . . . . . . . . .   3
   2.  The alt Namespace . . . . . . . . . . . . . . . . . . . . . .   3
   3.  IANA Considerations . . . . . . . . . . . . . . . . . . . . .   4
     3.1.  Special-Use Domain Name Registry  . . . . . . . . . . . .   4
     3.2.  Non-DNS Protocols Using the .alt Pseudo-TLD Registry  . .   4
   4.  Privacy Considerations  . . . . . . . . . . . . . . . . . . .   5
   5.  Security Considerations . . . . . . . . . . . . . . . . . . .   5
   6.  Acknowledgements  . . . . . . . . . . . . . . . . . . . . . .   5
   7.  References  . . . . . . . . . . . . . . . . . . . . . . . . .   5
     7.1.  Normative References  . . . . . . . . . . . . . . . . . .   5
     7.2.  Informative References  . . . . . . . . . . . . . . . . .   6
   Appendix A.  Changes / Author Notes.  . . . . . . . . . . . . . .   6
   Authors' Addresses  . . . . . . . . . . . . . . . . . . . . . . .   9

1.  Introduction

   Many Internet protocols need to name entities.  Names that look like
   DNS names (a series of labels separated with dots) have become
   common, even in systems that are not part of the global DNS
   administered by IANA.  This document reserves the root-level label
   "alt" (short for "alternative") as a special-use domain name
   ([RFC6761]).  This root-level label can be used as the final
   (rightmost) label to signify that the name is not rooted in the DNS,
   and that it should not be resolved using the DNS protocol.

   Throughout the rest of this document, the root-level "alt" label is
   shown as ".alt" to match the common presentation form of DNS names.

   The techniques in this document are primarily intended to address the
   "Experimental Squatting Problem", the "Land Rush Problem", and "Name
   Collisions" issues discussed in [RFC8244], which contains additional
   background on the issues with special use domain names.

1.1.  Requirements Notation

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
   "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this
   document are to be interpreted as described in [RFC2119].





Kumari & Hoffman        Expires 20 February 2023                [Page 2]

Internet-Draft               Reserve ALT TLD                 August 2022


1.2.  Terminology

   This document assumes familiarity with DNS terms; please see
   [RFC8849].  Terminology that is specific to this document is:

   *  DNS name: Domain names that are intended to be used with DNS
      resolution, either in the global DNS or in some other context.

   *  DNS context: The namespace anchored at the globally-unique DNS
      root, administered by IANA.  This is the namespace or context that
      "normal" DNS uses.

   *  non-DNS context: Any other (alternative) namespace.

   *  pseudo-TLD: A label that appears in a fully-qualified domain name
      in the position of a TLD, but which is not registered in the
      global DNS.  This term is not intended to be pejorative.

   *  TLD: The last visible label in either a fully-qualified domain
      name or a name that is qualified relative to the root.

2.  The alt Namespace

   This document reserves the .alt label for use as an unmanaged pseudo-
   TLD namespace.  The .alt label can be used in any domain name as a
   pseudo-TLD to signify that this is an alternative (non-DNS)
   namespace, and should not be looked up in a DNS context.

   Alternative namespaces should differentiate themselves from other
   alternative namespaces by choosing a name and using it in the label
   position just before the .alt pseudo-TLD.  For example, a group
   wishing to create a namespace for Friends Of Olaf might choose the
   string "foo" and use any set of labels under foo.alt.

   Because names beneath .alt are in an alternative namespace, they have
   no significance in the regular DNS context.  DNS stub and recursive
   resolvers do not need to look them up in the DNS context.

   DNS resolvers that serve the DNS protocol and non-DNS protocols at
   the same time might consider .alt like an entry in the "Transport-
   Independent Locally-Served DNS Zone Registry" that is part of IANA's
   "Locally-Served DNS Zones" registry, except that .alt is always used
   to denote names that are to be resolved by non-DNS protocols.








Kumari & Hoffman        Expires 20 February 2023                [Page 3]

Internet-Draft               Reserve ALT TLD                 August 2022


   Note that using .alt as a pseudo-TLD does not mandate how the non-DNS
   protocol will handle the name.  If the non-DNS protocol has a wire
   format like the DNS wire format, it might append the null label at
   the end of the name, but it also might not.  This document does not
   make any suggestion for how non-DNS protocols deal with the wire
   format of their names.

   Groups wishing to create new alternative namespaces may create their
   alternative namespace under a label that names their namespace under
   the .alt pseudo-TLD.  They should attempt to choose a label that they
   expect to be unique among similar groups and, ideally, descriptive.
   Developers are wholly responsible for dealing with any collisions
   that may occur under .alt.

   This document creates an IANA registry for specification documents
   that use the .alt pseudo-TLD.  The intention of the registry it to
   let developers of non-DNS protocols using the .alt pseudo-TLD know
   which other developers are using names under .alt.  It is possible
   for multiple different protocols to use the same names as each other.
   Because there is no requirement or expectation that developers of
   non-DNS protocols will use the registry, there is no priority given
   to names that appear in the directory.

   Currently deployed projects and protocols that are using pseudo-TLDs
   may choose to move under the .alt pseudo-TLD, but this is not a
   requirement.  Rather, the .alt pseudo-TLD is being reserved so that
   current and future projects of a similar nature have a designated
   place to create alternative resolution namespaces that will not
   conflict with the regular DNS context.

3.  IANA Considerations

3.1.  Special-Use Domain Name Registry

   The IANA is requested to add the .alt name to the "Special-Use Domain
   Name" registry ([RFC6761]), and reference this document.

3.2.  Non-DNS Protocols Using the .alt Pseudo-TLD Registry

   IANA is requested to create a new registry titled "Non-DNS Protocols
   Using the .alt Pseudo-TLD".  That registry description should point
   to this document.

   Entry to the registry is a combination of "Specification Required"
   and either "Expert Review" or "IESG Approval".  See [RFC8126] for the
   definition of these three terms,





Kumari & Hoffman        Expires 20 February 2023                [Page 4]

Internet-Draft               Reserve ALT TLD                 August 2022


   The registry will have two columns: "Reference" and "Name".  The
   "Reference" column gives a brief title and linked URL of the
   reference for the non-DNS protocol.  The "Name" column lists each
   name in the non-DNS protocol that would appear immediately to the
   left of the .alt pseudo-TLD.

4.  Privacy Considerations

   This document reserves .alt to be used to indicate that a name is not
   a DNS name, and so should not attempt to be resolved using the global
   DNS.  Unfortunately, these queries will undoubtedly leak into the
   global DNS.  This is a general problem with alternative name spaces
   and not confined to names ending in .alt.

5.  Security Considerations

   The unmanaged and "registration not required" nature of labels
   beneath .alt provides the opportunity for an attacker to re-use the
   chosen label and thereby possibly compromise applications dependent
   on the special host name.

6.  Acknowledgements

   We would like to thank Joe Abley, Mark Andrews, Erik Auerswald, Marc
   Blanchet, John Bond, Stephane Bortzmeyer, David Cake, David Conrad,
   Steve Crocker, Brian Dickson, Ralph Droms, Robert Edmonds, Patrik
   Faltstrom, Olafur Gudmundsson, Bob Harold, Joel Jaeggli, Ted Lemon,
   Edward Lewis, John Levine, George Michaelson, Ed Pascoe, Jim Reid,
   Arturo Servin, Paul Vixie and Suzanne Woolf for feedback.

   Christian Grothoff was also very helpful and deserves special
   recognition.

   In addition, Andrew Sullivan was an author from adoption (2015)
   through version 14 (2021).

7.  References

7.1.  Normative References

   [RFC2119]  Bradner, S., "Key words for use in RFCs to Indicate
              Requirement Levels", BCP 14, RFC 2119,
              DOI 10.17487/RFC2119, March 1997,
              <https://www.rfc-editor.org/info/rfc2119>.

   [RFC6761]  Cheshire, S. and M. Krochmal, "Special-Use Domain Names",
              RFC 6761, DOI 10.17487/RFC6761, February 2013,
              <https://www.rfc-editor.org/info/rfc6761>.



Kumari & Hoffman        Expires 20 February 2023                [Page 5]

Internet-Draft               Reserve ALT TLD                 August 2022


   [RFC8126]  Cotton, M., Leiba, B., and T. Narten, "Guidelines for
              Writing an IANA Considerations Section in RFCs", BCP 26,
              RFC 8126, DOI 10.17487/RFC8126, June 2017,
              <https://www.rfc-editor.org/info/rfc8126>.

7.2.  Informative References

   [RFC8244]  Lemon, T., Droms, R., and W. Kumari, "Special-Use Domain
              Names Problem Statement", RFC 8244, DOI 10.17487/RFC8244,
              October 2017, <https://www.rfc-editor.org/info/rfc8244>.

   [RFC8849]  Even, R. and J. Lennox, "Mapping RTP Streams to
              Controlling Multiple Streams for Telepresence (CLUE) Media
              Captures", RFC 8849, DOI 10.17487/RFC8849, January 2021,
              <https://www.rfc-editor.org/info/rfc8849>.

Appendix A.  Changes / Author Notes.

   [RFC Editor: Please remove this section before publication ]

   From -15 to -16:

   *  Many simplifications to focus the document on the technical bits
      as much as possible, based on mailing list feedback.

   *  Removed unused references.

   *  Removed the RFC 2119 language because it is no longer used in the
      document.

   *  Added a non-normative IANA registry.

   *  Added Paul Hoffman as second author to help get the draft moving
      in the DNSOP WG again.

   From -14 to -15:

   *  [Pinky]: Gee, Brain.  What are we going to do tonight?

   *  [The Brain]: The same thing we do every 6 months, Pinky.  Post a
      new version of this document, with only the version number
      changed.

   From -13 to -14:

   *  Andrew asked to be removed as co-author, due to potential
      perception of CoI.




Kumari & Hoffman        Expires 20 February 2023                [Page 6]

Internet-Draft               Reserve ALT TLD                 August 2022


   *  Erik Auerswald provided Github issues and comments re: references
      and grammar.

   From -12 to -13:

   *  Just bumping versions to prevent expiration.

   From -08 to -12:

   *  Just bumping versions to prevent expiration.

   *  Updated references (aggressive-nsec is now RFC 8198, draft-ietf-
      dnsop-sutld-ps is now 8244).

   From -07 to -08:

   *  Made it clear that this is only for non-DNS.

   *  As per Interim consensus, removed the "add this to local zones"
      text.

   *  Added a Privacy Considerations section

   *  Grammar fix -- "alternative" is more correct than "alternate",
      replaced.

   From -06 to -07:

   *  Rolled up the GItHub releases in to a full release.

   From -07.2 to -07.3 (GitHub point release):

      Removed 'sandbox' at Stephane's suggestion - https://www.ietf.org/
      mail-archive/web/dnsop/current/msg18495.html

      Suggested (in 4.1 bullet 3) that DNS libraries ignore these -- Bob
      Harold - https://mailarchive.ietf.org/arch/msg/dnsop/
      a_ruPf8osSzi_hCzCqOxYLXhYoA

      Added some pointers to the SUTLD document.

   From -07.1 to -07.2 (Github point release):

   *  Reverted the <TBD> string (at request of chairs).

   *  Added an editors note explaining the above.

   *  Removed some more background, editorializing, etc.



Kumari & Hoffman        Expires 20 February 2023                [Page 7]

Internet-Draft               Reserve ALT TLD                 August 2022


   From -06 to -07.1 (https://github.com/wkumari/draft-wkumari-dnsop-
   alt-tld/tree/7988fcf06100f7a17f21e6993b781690b5774472):

   *  Replaced ALT with <TBD> at the suggestions of George.

   From -05 to -06:

   *  Removed a large amount of background - we now have the (adopted)
      tldr document for that.

   *  Made it clear that pseudo-TLD is not intended to be pejorative.

   *  Tried to make it cleat that this is something people can choose to
      use - or not.

   From -04 to -05:

   *  Version bump - we are waiting in the queue for progress on SUN,
      bumping this to keep it alive.

   From -03 to -04:

   *  3 changes - the day, the month and the year (a bump to keep
      alive).

   From -02 to -03:

   *  Incorporate suggestions from Stephane and Paul Hoffman.

   From -01 to -02:

   *  Merged a bunch of changes from Paul Hoffman.  Thanks for sending a
      git pull.

   From -00 to 01:

   *  Removed the "delegated to new style AS112 servers" text -this was
      legacy from the omnicient AS112 days.  (Joe Abley)

   *  Removed the "Advice to implemntors" section.  This used to
      recommend that people used a subdomain of a domain in the DNS.  It
      was pointed out that this breaks things badly if the domain
      expires.

   *  Added text about why we don't want to adminster a registry for
      ALT.

   From Individual-06 to DNSOP-00



Kumari & Hoffman        Expires 20 February 2023                [Page 8]

Internet-Draft               Reserve ALT TLD                 August 2022


   *  Nothing changed, simply renamed draft-wkumari-dnsop-alt-tld to
      draft-ietf-dnsop-alt-tld

   From -05 to -06

   *  Incorporated comments from a number of people, including a number
      of suggestion heard at the IETF meeting in Dallas, and the DNSOP
      Interim meeting in May, 2015.

   *  Removed the "Let's have an (optional) IANA registry for people to
      (opportinistically) register their string, if they want that
      option" stuff.  It was, um, optional....

   From -04 to -05

   *  Went through and made sure that I'd captured the feedback
      received.

   *  Comments from Ed Lewis.

   *  Filled in the "Domain Name Reservation Considerations" section of
      RFC6761.

   *  Removed examples from .Onion.

   From -03 to -04

   *  Incorporated some comments from Paul Hoffman

   From -02 to -03

   *  After discussions with chairs, made this much more generic (not
      purely non-DNS), and some cleanup.

   From -01 to -02

   *  Removed some fluffy wording, tightened up the language some.

   From -00 to -01.

   *  Fixed the abstract.

   *  Recommended that folk root their non-DNS namespace under a DNS
      namespace that they control (Joe Abley)

Authors' Addresses





Kumari & Hoffman        Expires 20 February 2023                [Page 9]

Internet-Draft               Reserve ALT TLD                 August 2022


   Warren Kumari
   Google
   1600 Amphitheatre Parkway
   Mountain View, CA,  94043
   United States of America

   Email: warren@kumari.net


   Paul Hoffman
   ICANN

   Email: paul.hoffman@icann.org






































Kumari & Hoffman        Expires 20 February 2023               [Page 10]
```
