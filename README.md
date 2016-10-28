About SBO Downloader
==============

SBODownloader is a Python script for create EPUB files by downloading Safari Books Online contents. It's capable of writing EPUB files programmatically.

Sphinx documentation is generated from the templates in the docs/ directory and made available at http://ebooklib.readthedocs.org

Usage
=====

Reading
-------

    import ebooklib
    from ebooklib import epub

    book = epub.read_epub('test.epub')

    for image in book.get_items_of_type(ebooklib.ITEM_IMAGE):
        print image

Writing
-------

    from ebooklib import epub

    book = epub.EpubBook()

    # set metadata
    book.set_identifier('id123456')
    book.set_title('Sample book')
    book.set_language('en')

    book.add_author('Author Authorowski')
    book.add_author('Danko Bananko', file_as='Gospodin Danko Bananko', role='ill', uid='coauthor')

    # create chapter
    c1 = epub.EpubHtml(title='Intro', file_name='chap_01.xhtml', lang='hr')
    c1.content=u'<h1>Intro heading</h1><p>Zaba je skocila u baru.</p>'

    # add chapter
    book.add_item(c1)

    # define Table Of Contents
    book.toc = (epub.Link('chap_01.xhtml', 'Introduction', 'intro'),
                 (epub.Section('Simple book'),
                 (c1, ))
                )

    # add default NCX and Nav file
    book.add_item(epub.EpubNcx())
    book.add_item(epub.EpubNav())

    # define CSS style
    style = 'BODY {color: white;}'
    nav_css = epub.EpubItem(uid="style_nav", file_name="style/nav.css", media_type="text/css", content=style)

    # add CSS file
    book.add_item(nav_css)

    # basic spine
    book.spine = ['nav', c1]

    # write to the file
    epub.write_epub('test.epub', book, {})



License
=======

EbookLib is licensed under the AGPL license.


Authors
=======

Full list of authors is in AUTHORS.txt file.
