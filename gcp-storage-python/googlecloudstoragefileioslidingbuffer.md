---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.fileio.SlidingBuffer
fetched_at: 2026-01-25T15:27:36.594781
---

# Class SlidingBuffer (3.7.0)

`SlidingBuffer()`


A non-rewindable buffer that frees memory of chunks already consumed.

This class is necessary because `google-resumable-media-python`

expects
`tell()`

to work relative to the start of the file, not relative to a place
in an intermediate buffer. Using this class, we present an external
interface with consistent seek and tell behavior without having to actually
store bytes already sent.

Behavior of this class differs from an ordinary BytesIO buffer. `write()`

will always append to the end of the file only and not change the seek
position otherwise. `flush()`

will delete all data already read (data to the
left of the seek position). `tell()`

will report the seek position of the
buffer including all deleted data. Additionally the class implements
**len**() which will report the size of the actual underlying buffer.

This class does not attempt to implement the entire Python I/O interface.

## Methods

### __len__

`__len__()`


Determine the size of the buffer by seeking to the end.

### flush

`flush()`


Delete already-read data (all data to the left of the position).

### read

`read(size=-1)`


Read and move the cursor.

### seek

`seek(pos)`


Seek to a position (backwards only) within the internal buffer.

This implementation of seek() verifies that the seek destination is contained in _buffer. It will raise ValueError if the destination byte has already been purged from the buffer.

The "whence" argument is not supported in this implementation.

### tell

`tell()`


Report how many bytes have been read from the buffer in total.

### write

`write(b)`


Append to the end of the buffer without changing the position.