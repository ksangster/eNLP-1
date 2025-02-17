.. note::
    :class: sphx-glr-download-link-note

    Click :ref:`here <sphx_glr_download_examples_ex_nlp_pipeline.py>` to download the full example code
.. rst-class:: sphx-glr-example-title

.. _sphx_glr_examples_ex_nlp_pipeline.py:


NLP Pipeline
============
The following example takes a raw extract of norwegian texts, removes stopwords and lemmatizes prior to analysing the
distribution of the words in the text.


.. code-block:: default


    import matplotlib.pyplot as plt
    plt.close('all') # very important for read the docs to avoid it crashing due to memory

    from enlp.processing.stdtools import get_stopwords, tokenise
    from enlp.pipeline import nlp_pipeline
    from enlp.visualisation.freq_distribution import wordcloud_plot

    import spacy









Load Spacy's Norwegian language model and the example text


.. code-block:: default

    langmodel = spacy.load('nb_dep_ud_sm')
    with open("example_data/no_den_stygge_andungen.txt", "r") as file:
        text = file.read()
    text = text.replace('\n', ' ')







Get a list of stopwords to be removed from the text


.. code-block:: default


    # Get stopwords
    all_stopwords, stopwords_nb, stopwords_en = get_stopwords()







Using NLP pipeline class to create a processing workflow. The pipeline shall involve:
- remove punctuation
- remove stopwords
- stem remaining words


.. code-block:: default


    # Initialise object
    processed_text = nlp_pipeline(langmodel, text)

    # Run processing as a pipeline
    processed_text.rm_punctuation().rm_stopwords(stopwords=all_stopwords).nltk_stem_no()







Compare text strings of firs 80 characters of the original and processed.


.. code-block:: default


    print ('Original: ', text[:80], '...')
    print ('Processed: ', processed_text.text[:80], '...')






.. rst-class:: sphx-glr-script-out

 Out:

 .. code-block:: none

    Original:  Den stygge andungen Det var så deilig ute på landet; det var sommer, kornet stod ...
    Processed:  stygg andung deil ute somm korn stod gult havr grønn høyet reist stakk ned grønn ...



Wordcloud comparison between most common words


.. code-block:: default

    fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(10, 5))
    wordcloud_plot(tokenise(langmodel,text), ax=ax1)
    wordcloud_plot(processed_text.tokenise().tokens, ax=ax2)
    plt.tight_layout()





.. image:: /examples/images/sphx_glr_ex_nlp_pipeline_001.png
    :class: sphx-glr-single-img





.. rst-class:: sphx-glr-timing

   **Total running time of the script:** ( 0 minutes  8.964 seconds)


.. _sphx_glr_download_examples_ex_nlp_pipeline.py:


.. only :: html

 .. container:: sphx-glr-footer
    :class: sphx-glr-footer-example



  .. container:: sphx-glr-download

     :download:`Download Python source code: ex_nlp_pipeline.py <ex_nlp_pipeline.py>`



  .. container:: sphx-glr-download

     :download:`Download Jupyter notebook: ex_nlp_pipeline.ipynb <ex_nlp_pipeline.ipynb>`


.. only:: html

 .. rst-class:: sphx-glr-signature

    `Gallery generated by Sphinx-Gallery <https://sphinx-gallery.github.io>`_
