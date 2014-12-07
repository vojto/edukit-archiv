# Otvorenie suboru z prvej prednasky

    import IOExtensions

    code fromf tof cf = (readBinaryFile fromf) >>= (return . map cf) >>= (writeBinaryFile tof)

    codech c = chr ((ord c+2) `mod` 256)

    encodech c = chr ((ord c+254) `mod` 256)

    codefile = code "ZFP.pdf" "ZFP.zip" codech

    encodefile = code "ZFP.zip" "ZFPn.pdf" encodech