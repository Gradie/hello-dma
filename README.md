# hello-world
Just another repository
hi humans!
#ifndef _ADMA_H_INCLUDE
#define _ADMA_H_INCLUDE

#define A_DMA_IGET(mode,src,dest,len,re_addr)\
({
	dma_desc __da__=0;\
	dma_set_op(&__da__,DMA_GET);\
	dma_set_mode(&__da__,mode);\
	dma_set_size(&__da__,len);\
	dma_set_reply(&__da__,re_addr);\
	dma(__da__,src,dest);\
})
/*backup athread_get*/
#define A_DMA_GET(mode,src,dest,len,re_addr)\
({
	dma_desc __da__=0;\
	dma_set_op(&__da__,DMA_GET);\
	dma_set_mode(&__da__,mode);\
	dma_set_size(&__da__,len);\
	dma_set_reply(&__da__,re_addr);\
	dma(__da__,src,dest);\
	dma_wait(re_addr,1);
})

#define A_DMA_GET_SET(da,mode,len,re_addr)\
({
	dma_set_op(&da,DMA_GET);\
	dma_set_mode(&da,mode);\
	dma_set_size(&da,len);\
	dma_set_reply(&da,re_addr);
})

#define A_DMA_GET_RUN(da,src,dest)\
({
	dma(da,src,dest);
})

#define A_DMA_GET_WAIT(re_addr,n)\
({ 
	dma_wait((re_addr),n);
})

#define A_DMA_PUT_SET(da,mode,len,re_addr)\
({
	dma_set_op(&da,DMA_PUT); \
	dma_set_mode(&da,mode); \
	dma_set_size(&da,len); \
	dma_set_reply(&da,re_addr);
})

#define A_DMA_PUT_RUN(da,src,dest)\
({
	dma(da,src,dest);
})

#define A_DMA_PUT_WAIT(re_addr,n)\
({ 
	dma_wait((re_addr),n);
})

#endif // !_ADMA_H_INCLUDE
