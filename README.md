# Pragyan2020-Forensics-Encuentralo_si_puedes

![image](https://user-images.githubusercontent.com/54376366/75124642-ddc01b00-566d-11ea-90f4-2ab5450558fb.png)


There are 4 files given: 3 encrypted PDFs and one MP3.<br>
![image](https://user-images.githubusercontent.com/54376366/75102110-8e151d00-55a3-11ea-828e-08313da16504.png)

Listening to the MP3 file reveals there is a morse code at the beginning and end of the Despacito song.

Cutting everything but morsecode sounds in Audacity, and maxing out the gain since some of it is very low volume, https://morsecode.world/international/decoder/audio-decoder-adaptive.html output the following message:
`/BRUTE/DE/CINCO/DIGITOS/CON/MINUSCULAS/Y/NUMEROS`

Pdfcrack.exe is able to brute force the 3 PDF files:
```
.\pdfcrack.exe -f 1Hola.pdf -c 0123456789abcdefghijklmnopqrstuvwxyz -n 5 -m 5
found user-password: 'x2n1z'

.\pdfcrack.exe -f 2Mi.pdf -c 0123456789abcdefghijklmnopqrstuvwxyz -n 5 -m 5
found user-password: '39adz'

.\pdfcrack.exe -f 3Amigo.pdf -c 0123456789abcdefghijklmnopqrstuvwxyz -n 5 -m 5
found user-password: '8yfa2'
```

1Hola.pdf and 2Mi.pdf are the same PDFs found on http://shattered.io/ - http://shattered.io/static/shattered-1.pdf and http://shattered.io/static/shattered-2.pdf

3Amigo.pdf contains a message: ` SHA1[original files] = base64-decrypt(base64-decrypt(flag))`

Getting a SHA1 hash of either Shattered PDFs retrieves the following:
```
> (Get-FileHash .\shattered-1.pdf -Algorithm SHA1).Hash.toLower()
> 38762cf7f55934b34d179ae6a4c80cadccbb7f0a
```
Base64 Encoding the hash 2 times returns TXpnM05qSmpaamRtTlRVNU16UmlNelJrTVRjNVlXVTJZVFJqT0RCallXUmpZMkppTjJZd1lRPT0=.

<b>p_ctf{TXpnM05qSmpaamRtTlRVNU16UmlNelJrTVRjNVlXVTJZVFJqT0RCallXUmpZMkppTjJZd1lRPT0=}</b>
