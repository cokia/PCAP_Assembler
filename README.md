#PCAP Assembler with CPP

##서문 
사실 Python이나 C#쓰면 겁나쉬운건데 살면서 처음다뤄보는 CPP로 해보는 첫 프로젝트입니다


##사용 라이브러리
라이브러리같은거 키우는 취미없어요. 오직 **노가다** 뿐이죠.

~~사실 라이브러리 쓸줄몰라서 이러는건 안비밀!~~

##사용법
뭐 복잡한거 없어요! 겁나게 쉬워요 , 간지나게 터미널 **빡** 하고 켜주세요.
이렇게 쳐주세요!

그리고 PCAP Assembler가 있는 경로를 들어가서 `./Fpcap`
**빡** 누르면  에러가 ***뿜뿜*** 할거에요.그러니까 `./Fpcap Desktop/doghunnyjam.pcap` 요로코롬 하세요 
**참 쉽죠?**


##딱히 너보라고 쓰는 정리는 아니라구! 흥!
```

// #define MAGIC   0xa1b2c3d4 

// Ethernet addresses are 6 bytes
#define ETHER_ADDR_LEN	6

	/* Ethernet header */
	struct sniff_ethernet {
		u_char ether_dhost[ETHER_ADDR_LEN]; // Destination host address
		u_char ether_shost[ETHER_ADDR_LEN]; // Source host address
		u_short ether_type; /* IP? ARP? RARP? etc */
	};

	/* IP header */
	struct sniff_ip {
		u_char ip_vhl;		// version << 4 | header length >> 2 
		u_char ip_tos;		// type of service 
		u_short ip_len;		// total length 
		u_short ip_id;		// identification 
		u_short ip_off;		// fragment offset field 
	#define IP_RF 0x8000		// reserved fragment flag 
	#define IP_DF 0x4000		// dont fragment flag 
	#define IP_MF 0x2000		// more fragments flag 
	#define IP_OFFMASK 0x1fff	// mask for fragmenting bits 
		u_char ip_ttl;		// time to live 
		u_char ip_p;		// protocol 
		u_short ip_sum;		// checksum 
		struct in_addr ip_src,ip_dst; // source and dest address 
	};
	#define IP_HL(ip)		(((ip)->ip_vhl) & 0x0f)
	#define IP_V(ip)		(((ip)->ip_vhl) >> 4)

	/* TCP header */
	typedef u_int tcp_seq;

	struct sniff_tcp {
		u_short th_sport;	/* source port */
		u_short th_dport;	/* destination port */
		tcp_seq th_seq;		/* sequence number */
		tcp_seq th_ack;		/* acknowledgement number */
		u_char th_offx2;	/* data offset, rsvd */
	#define TH_OFF(th)	(((th)->th_offx2 & 0xf0) >> 4)
		u_char th_flags;
	#define TH_FIN 0x01
	#define TH_SYN 0x02
	#define TH_RST 0x04
	#define TH_PUSH 0x08
	#define TH_ACK 0x10
	#define TH_URG 0x20
	#define TH_ECE 0x40
	#define TH_CWR 0x80
	#define TH_FLAGS (TH_FIN|TH_SYN|TH_RST|TH_ACK|TH_URG|TH_ECE|TH_CWR)
		u_short th_win;		/* window */
		u_short th_sum;		/* checksum */
		u_short th_urp;		/* urgent pointer */
};
```
##참고문헌
https://www.tcpdump.org/pcap.html
