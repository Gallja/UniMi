Il L2 di Ethernet è multi-layer, in particolare 2:
- MAC Media Access Control: funzionalità di Carrier Sense, BEB, Collision Control. Definisce delle primitive
	Ogni scheda ethernet ha un indirizzo MAC unico di 48 bit
- LLC Logical Link Control: si basa su [[HDLC]] 
	A livello LLC sono interessato a ipotizzare la comunicazione da sorgente a destinatario. Supporta sia la modalita best-effort connectionless sia quella affidabile connection-oriented
	Il network layer utilizzerà i servizi concessi dal MAC sublayer.