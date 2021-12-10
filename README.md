   This is a novel about Dinos
   
    { # Final2Novel
    Novel about Dinos



    text = open("/content/dinos.txt", "r").read()


    # let's install weasyprint!
    !pip install weasyprint==52.5

    # also we need markdown
    import markdown


    import random

    def altchapter():
     ngrams = {}
     d = 4


     for i in range(len(text)-d-1):
    stem = text[i:i+d]
    twig = text[i+d]

    if (stem not in ngrams.keys()):
      ngrams[stem] = [twig]
    else:
      ngrams[stem].append(twig)

      seed = random.choice(list(ngrams.keys()))
      new_text = seed
    #print(seed)
    for i in range(10000000000):
    root = new_text[-d:]
    if(root in ngrams.keys() and len(ngrams[root]) > 0):
      pick = random.randrange(len(ngrams[root]))
      new_text += ngrams[root][pick]
      ngrams[root].pop(pick)

    return(new_text)


    import random
    text = open("/content/dinos.txt", "r").read()
    ngrams = []

    for b in range(len(text) - 8):
     ngrams.append(text[b:b+8])

    random.shuffle(ngrams)
    seed = random.choice(ngrams)

    new_text = seed

    for i in range(500):
    for n in ngrams:
    if (n[7] == new_text[-7]):
      new_text += n[-1]
      

      print(new_text)


    import random

    novel = """


    # Dinosaurs are cool : a novel
    ### by Victoria Percherke


    """

    for chapter in range(1,10):
 

     ## Chapter {chapter}

      novel+= altchapter()


    # convert the markdown formatted novel string into html
    # also we need markdown
    import markdown
    html = markdown.markdown(novel)
    from weasyprint import HTML, CSS
    from weasyprint.fonts import FontConfiguration



      # prepare WeasyPrint
    font_config = FontConfiguration()
    rendered_html = HTML(string=html)

    css = CSS(string='''
    @import url('https://fonts.googleapis.com/css2?family=Festive&display=swap');

    @import url('https://fonts.googleapis.com/css2?family=Merriweather:wght@300&display=swap');
    body {
    font-family: 'Times New Roman', serif;


      hr {
    break-after: recto; 


    h1 {
     font-size: 50pt;
    text-align:center;
    margin-top: 3in;
    font-family: 'Festive',cursive;
    }
    h2{
      break-before: recto;
      font-family: 'Festive',cursive;


    h3 {
      font-size: 20pt;
      text-align:center;


    /* set the basic page geometry and start the incrementer */
    @page {
      font-family: 'Times New Roman', serif;
      margin: 1in;
      size: letter;
      counter-increment: page;
      @bottom-center {
        content: "Laugh Track";
        text-align:center;
        font-style: italic;
        color: #666666;



    /* print the page number on the bottom-right of recto pages */
    @page :right {
      @bottom-right{
        content: "[" counter(page) "]";
        text-align:right;
        color: #666666;
        visibility: invisible;



    /* print the page number on the bottom-left of verso pages */
    @page :left {
      @bottom-left{
        content: "[" counter(page) "]";
        text-align:left;
        color: #666666;



    /* blank the footer on the first page */
    @page:first{
      @bottom-left {content: ""}
      @bottom-right {content: ""}
      @bottom-center {content: ""}



    ''', font_config=font_config)

    # Finally, this creates a PDF called "example.pdf" with all the above settings
    rendered_html.write_pdf('/content/example.pdf', stylesheets=[css],font_config=font_config)

    }
