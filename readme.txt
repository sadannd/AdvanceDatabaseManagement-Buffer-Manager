Group Memebers:

    1.  Name  : Shikhar Saraswat
        Email : ssaraswat@hawk.iit.edu
        CWID  : A20514418

    2.  Name  : Sadanand Kohle
        Email : skolhe1@hawk.iit.edu
        CWID  : A20517969
        

    3.  Name  : Vidhi Sanghavi
        Email : vsanghavi@hawk.iit.edu
        CWID  : A20467207
        


Project Structure:

assign2
    README .md
    Makefile
    buffer_mgr .h
    buffer_mgr_stat .c
    buffer_mgr_stat .h
    dberror .c
    dberror .h
    dt.h
    storage_mgr .h
    test_assign2_1 .c
    test_assign2_2 .c
    test_helper .h

Project Summary
------------------------------------------------------------------


Steps For Running Assignment1
------------------------------------------------------------------

1) Go to Project root (assign1) using Terminal.

2) Type ls to list the files and check that we are in the correct directory.

3) Type "make clean" to delete old compiled .o files.

4) Type "make" to compile all project files including "test_assign2_1.c" & "test_assign2_1.c" file 

5) Type ./test1 to execute test cases.

Function Description
------------------------------------------------------------------

 RC initBufferPool ( BM_BufferPool * const bm , const char * const pageFileName ,
 const int numPages , ReplacementStrategy strategy ,
 void * stratData );
 creates a new buffer pool with numPages page frames using the page replacement
 strategy strategy. The pool is used to cache pages from the page file with name pageFileName.
 Initially, all page frames are empty. The page file already exist, i.e., this method
 does not generate a new page file. stratData used to pass parameters for the page
 replacement strategy.

 RC shutdownBufferPool ( BM_BufferPool * const bm);
 destroys a buffer pool and free up all resources associated
 with buffer pool.
	
 RC forceFlushPool ( BM_BufferPool * const bm);
 causes all dirty pages (with fix count 0) from the buffer pool to be written to
 disk.

 // Buffer Manager Interface Access Pages
 RC markDirty ( BM_BufferPool * const bm , BM_PageHandle * const page );
 marks a page as dirty

 RC unpinPage ( BM_BufferPool * const bm , BM_PageHandle * const page );
 unpins the page page.

 RC forcePage ( BM_BufferPool * const bm , BM_PageHandle * const page );
 write the current content of the page back to the page file on disk.

 RC pinPage ( BM_BufferPool * const bm , BM_PageHandle * const page , const PageNumber pageNum );
    pins the page with page number pageNum. The buffer manager sets the pageNum field of the page handler passed to the method. 
 
 // Statistics Interface
 PageNumber * getFrameContents ( BM_BufferPool * const bm);
 bool * getDirtyFlags ( BM_BufferPool * const bm);
 int * getFixCounts ( BM_BufferPool * const bm) ;
 int getNumReadIO ( BM_BufferPool * const bm);
 int getNumWriteIO ( BM_BufferPool * const bm) ;

 3. STATISTICS FUNCTIONS
===========================

The statistics related functions are used to gather some information about the buffer pool.

getFrameContents(...)

-> This function returns a list of PageNumbers as an array. 
->We interate through all pages from buffer pool.

getDirtyFlags(...)
-> This function return array of boolean flags and size is equal to number of pages. To get this data we iterate through all page frames in buffer pool.

getFixCounts(...) 
->This function return array of ints. Here also to get this data we iterate through all page frames in buffer pool.

getNumReadIO(...)
->Return total number of IO reads performed by the buffer pool. Means total number of pages read from disk.

getNumWriteIO(...) 
->Return total number of IO write performed by the buffer pool. Means total number of pages written on disk.
—> The numPage variable is used to keep track of this information initiaising with zero and incrementing for every write.


4. PAGE REPLACEMENT ALGORITHMS
=================

FIFO(...)
-> First In First Out (FIFO).
-> The page which enter first will be at first position and appended next pages in sequnce. When buffer is full then first inserted page will be replaced. And content of old page moved to disk.

LFU(...)
-> Least Frequently Utilized (LFU). Re,ove page which is not used frquently when buffre size is full.
-> For each page we have lfuIndex which keep track of the count  of how many page frames the user has accessed.
-> When buffer is full we have to indetify page frame with lowest lfuIndex and replace it with new one and move old page frame to disk.

LRU(...)
-> Least Recently Used (LRU). algorithm is a page replacement technique used for memory management..
-> According to this method, the page which is least recently used is replaced.
-> Any page that has been unused for a longer period of time than the others is replaced.

CLOCK(...)
->The clock algorithm keeps a circular list of pages in memory, with the "hand" (iterator) pointing to the last examined page frame in the list. 
->When a page fault occurs and no empty frames exist, then the R (referenced) bit is inspected at the hand's location.

