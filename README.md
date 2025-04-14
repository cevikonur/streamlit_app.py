```python
import streamlit as st
import fitz  # PyMuPDF

st.title("K ve S Maddelerini Ayıklama Aracı")

pdf_dosya = st.file_uploader("PDF dosyasını yükle", type="pdf")

if pdf_dosya:
    doc = fitz.open(stream=pdf_dosya.read(), filetype="pdf")
    metin = ""
    for sayfa in doc:
        metin += sayfa.get_text()

    k_maddeleri = [satır for satır in metin.splitlines() if satır.strip().startswith(("K", "(K"))]
    s_maddeleri = [satır for satır in metin.splitlines() if satır.strip().startswith(("S", "(S"))]

    st.subheader("K Maddeleri")
    for madde in k_maddeleri:st.write(madde)

    st.subheader("S Maddeleri")
    for madde in s_maddeleri:
        st.write(madde)
