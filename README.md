# Using DNS To Store Image Files

This is a simple example of how one might store an image on a DNS server using TXT records.  This may be useful for redundancy or to insure that an image remains available for an extended period of time without requiring a webserver to provide the image data.  For example, a domain's registration may be pre-paid to last for the next 10 years, which would insure that the data is available online for the next 10 years regardless of whether the domain is currently hosting a website.

The maximum length of data stored in this manner using base64 encoding is 3,000 bytes.

To display an image stored in a DNS TXT record, a server-side application must use a DNS lookup tool such as dig to retrieve the TXT record, and then concatenate the records in the reverse order in which they are returned from the DNS server and return the concatenated data to the user's browser, which may be loaded as base64 encoded data inside of an IMG tag pointing to the retrieval service.  Multiple TXT records are stored left-to-right on a single line in BIND as they are added to a DNS server, and so the ordering is preserved for re-assembly.  

For my example I have stored this image:     
![103-1038880_user-rubber-stamp-female-user-icon-min](https://user-images.githubusercontent.com/48937881/154846348-5072f1b3-6923-4a9b-86d2-6048ae4a5b73.png)


An example of retrieving this data follows, using the Linux dig command to retrieve the record:
```
amrita@localhost:~$ dig nft.bithi.me TXT

; <<>> DiG 9.16.1-Ubuntu <<>> nft.bithi.me TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 48344
;; flags: qr rd ra; QUERY: 1, ANSWER: 15, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;nft.bithi.me.			IN	TXT

;; ANSWER SECTION:
nft.bithi.me.		300	IN	TXT	"uJzgzA/r1voHcb0SnEZXfxCoPpP3mCMKTWKXwjY5YKPxnvOCMtz9ZKmeIynjNBs2uXrpuI3PFxHNu3Gi7PS6Z4wxubRbr2Pl/+185I8o9Td9/G1X3frHMJ3VaX77+MN58I6wxiYpO/QC+bSxb4dNouzC8wdfFWuSx3VMcaQQw2deOlfsaGP+4heK0rMnfp8QZWzurd7iJ4RmcpOfiOBCsxbfuVanIPX/lvh/EMMbIlJ8ElJzYl5QU4XMeNwZaur"
nft.bithi.me.		300	IN	TXT	"9TIkjTNMKjNrqeSUy/QuUCcWJqzAdLHHgNQS7JPIOQSajQWQAhao9M+2JBFCr3wPNqnUN42MaBMrd+iWoP9sUCTS7Eqt2uggoFeArxgZytALLWX2Q41Faob6B/mpreTXjcVrbrwuFnucIGsYWkVZB9kXtqxnoOGfT4CChqyH1bnV9QVDsLtcOgLf6eQ8hN4DLJODOuPNiClFBGeKGhSd7T4AudZSMIr7UBeVIl27QAbzF8EqRKthbjNtJLkJUto"
nft.bithi.me.		300	IN	TXT	"oHSAPVtvVEV6/bhYITT4EWu/ywZ3mOEz5JR+mmrNCHRKdsPhKMaT6xBiHQX3PtPNh6gGrVeMgxVD/HaawpcS3BuFy3ImJD1S2ytGj4zN8MYOCLttSdi3UmwJuCiBKKNzI0qyQ4rESpYfgiMTcR1XysoLkz0MlEuEhOVZIDgjelFphHn8envICLWvk1Euc5ey9+vcPdFbSmVXHJUHr4OCQVpjH10OJ9rmrrDL+5E940GTH2BpkHhik/uXixHQn9C"
nft.bithi.me.		300	IN	TXT	"1dTTu+AW03AQ7RwuLTxUy5w/N/sFRA14M64KpqWpi9PZmxinwjqtrgSxzOq06HMwbq/G3k/rzG1JvtaskHWrtLYgLTH+TI6GRgwYl8lmlOQuvVnn4H6PcGtk8/hsCF4WGMV+2lx/aePb1rLNokY+kLAVBmCcfq21lDMp8ly1meZvEM2wASVhtjz+KSQdITWih6eKHSkodpCRDTgDqdvlKxgTGl2DggvbuGaoL/a7xwd3K4CZITDhdP5UcUpFhhe"
nft.bithi.me.		300	IN	TXT	"3nw8Vwej0R4m1bn6KeNRsN3vI99+byeF2FD/lt8z/o2JyLM5fEPQBmXqLB3Y460TgTCGvitysApo/78K8wptr1vcqGMyKxABvZHvFlpm2ydaM0KGUFOSr6noCjl4/RFECpN3WmNWYdp8GZlicCstIwCA1mJhVRaIx//zOa9UD8hB85Yve4vQ2ENPp/Inw7hOrsX4Q3kRAi9aqymfh5sRR4Wcp67WZ+oVospaxqfaw8/qrWYD1tl+CCNgzyCNGWs"
nft.bithi.me.		300	IN	TXT	"RAyP4JhYccYczGpyoJSBJj276lsRD1P+BZ53J5fC5Yhq1afB5/goH0zsPm5y11k1n3K5HHx0FfmoHN43+A/wclqgoshNhowtZbLrDR5X6JasZp6EvgNP4M/E+SgJxmIUG5OIhyAtsbKwG5BH0xHCQV/h+VgJzlIod5Tx0h1C6St/Q4yI8ku0pXkNNW57dT5QBJs+YUMU4g+9zYrhSrX+p5Um0HuTPa2rfPyXYd4CDpTh7893wwelEtghROsXVFO"
nft.bithi.me.		300	IN	TXT	"hiwR5h9H1xgbe79vGQbMoQgi/mzZ/bhtHW9qjYH/SGfcL5+l/wabs1vADG2wTNg4HAUYHjbQo4BCMy+lK9K20gYXjDsPT+p7mlJHegwQYmzMaJxPEB0qnKXYMQQxvwuaMN0CIl7dzENN8sFu5WEg7KFBgpjNI2RsEMdGAhZSCXfhdKwfRg28fWoGF0FtRGLW/SgpCJS+EAYtMWEj9BPCatRykGlTxLQU+xY5lAuvLUpCHjK1EKoaBUB9DivOAg5"
nft.bithi.me.		300	IN	TXT	"XSGOLdrYT0hJFYswGtf6BZxPZOdjlVEZAbdzARM0n0UQv0LHeIrKXf8iD4nDBOs3wR5NqxVo/D2IFYfWYyAnmFi3HptO3F4VhHqRR9uPgTT/AUKabAEkFW44yoyBJMMMn95vx0eGqrtrArtEx8K1/8RA6P1w7Xc8hFoFqnDFIrGSTOnUzZSf2va0H34lljywSLMUNkjVSIIIqcZBrvkSsrvO88PmMII8jYM0vUYQA+4zEOQec7qDbBl5d0nb/H7"
nft.bithi.me.		300	IN	TXT	"ZVKB43PDwZrkmHvp81b2Gn8v1KYLTSVPBaL+ZvJPj7ICwK7kWkPodADDtfaQ4ysAMt2KFhtrdk/AgMZpbWHtEbC6QiFHaQQFtIryyHiaAhjzaDcKgzqkr1DHSB9KhwiHbQxPa+LIYbdMHaJwgFS0RtN0u0HgcSp7+8cbG+/7jqGU5vh/JpWEUT5G4IIyHAM0O75oUmm14p15+72ELE6ZjkGhnf6EsRLFRyEFeELYM3nN1v9OS/C15gHHW9gRZML"
nft.bithi.me.		300	IN	TXT	"qiYfP9YylauIVnfJxDyBi1cGvUJ8HKkGv1UhpPp/cAudqqbBBCamYQLtpvy0UOj4oBGety1CwBeTIaLvlILvZuGf6uIOQpsVetj4L9CC7EQ1o/Q7p0X+xC1ZsIl22xSuy6nyDpmduIg9AX/MDqptv56apXXUOCS+zig5xBsO3xZh5iM3LycbDy6CY7P327m2uI7LLAGLbAX20SCEvoQ5vftykjtR2Gv03Ze7dT1o1/dWvywd9LaP4B2s6r6hbB2"
nft.bithi.me.		300	IN	TXT	"5expf/i5iTPixiV/y000BWI3/vIzfGu2Nd9B1bxbRbkBKJqGH+PEDwb4++UhK52eXCPb/8XokLCPv0C4hD8fDwK7bqgUXy5dK25V55YKbqT+AHtuwn2kXkHK0jl5xSoGEUNEyJ7ZrrdBAUqkD0FqKJCANTDPWvYeMRDKFDlpYxdddCXTCIPxOAQQ9Bh26Rn3xZTg3/rGBm4+DsEfs3dCKD2FIz6PttACsmU04beOq+Qlpi/kiWsvMKk5P2S6RMp"
nft.bithi.me.		300	IN	TXT	"dSbcxSZV9o7XWE7QujK64xD9uTHM1T0WXlaapXXCrLm69Hlm4LAjzR2E0OXLuqArn1+eqRVsg7rJZGpvN5ma1IJtbcmO7MeseEGxuQMQ2njp1+iy7hHXlfwDrbuT8nXEnNmLF8+d9eHmwzk1apuAqH5e3QuNH3S8FQ/BiVz9jueQ1EzP1NlEU6c4MTNQKLo9piTIeVHX356PpNAvUo4VYYzy1IUjxQjao+bvRnl+isxeQ8jXk+v4u24+9BI6936"
nft.bithi.me.		300	IN	TXT	"z0jLP99iOV/C0Kbjc0V926dTUlKSj6TXVzeaDDT3oWoKm6c3PbO8N5+JME0sktQ2NTNKVllKm9BlEXJS8P8CUzrMiQ8IU/hBsTItDYd09rYI/ZAz3TUn/17X5KQbi/MPS5nLtMzF7Xg5iM0zvaVyt8+QsbNJgsaMXPl7oSUk6eOJe79YtaoPj5cBxm6MUfp7HlqnEGo3Kj+7Dw+oeH70gvlSso6jlLW3L0Ss3SYL7ecz26oOgWhq74ZyC7hlS1Z"
nft.bithi.me.		300	IN	TXT	"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAGQAAABkCAAAAABVicqIAAAKkUlEQVRo3tWaeVwTVx7AZwKCSl2lpd6lqOyKVld3W91at65+rFt1/dS2Xuu6q1tqadXaelWFT73a6qp4dD9aASuHCireKyptRdBV0MopKiIiSLiSTMKREEhCJu7vzUwyM8mbJJDs57P7/klm3pv3nffmd88QzyyoGTVMMzIHlgbmQMce6JiDBkvnx"
nft.bithi.me.		300	IN	TXT	"T0pcfxyjyEv4YDBW1nyC/xx7q85rn/mUZR3dMPmXfKQt6zl4wtrEn0qU3v5gyaB+VJR5LP5gXHxKRmGpqs3bHyz9X3zfJf05XIubEJfjnv0HieqmfRQ8f+0AAAAASUVORK5CYII="

;; Query time: 508 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sun Feb 20 05:56:41 PST 2022
;; MSG SIZE  rcvd: 3942
```

![image](https://user-images.githubusercontent.com/48937881/154846298-6f537240-3034-4c61-97b2-791aef906d9f.png)
