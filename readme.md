#TwainForC#

###About TwainForC# 
This is the base TWAIN class.  It's versioned so that developers can
safely make a reference to it, if they don't want to actually include
the TWAIN modules in their project.

###Our Goals
	- Make the interface better than raw TWAIN (like with C/C++), but don't
		go as far as making a toolkit.  Expose as much of TWAIN as possible.
		Part of this involves making a CSV interface to abstract away some of
		the pain of the C/C++ structures, especially TW_CAPABILITY.
      
	- Use type checking wherever possible.  This is why the TWAIN contants
		tend to be enumerations and why there are multiple entry points into
		the DSM_Entry function.
      
	- Avoid unsafe code.  We use marshalling, and we're forced to use some
		unmanaged memory, but that's it.
      
	- Run thread safe.  Force as many TWAIN calls into a single thread as
		possible.  The main exceptions are MSG_PROCESSEVENT and any of the
		calls that unwind the state machine (ex: MSG_DISABLEDS).  Otherwise
		all of the calls are serialized through a single thread.
      
	- Avoid use of System.Windows content, so that the TWAIN assembly can be
		used as broadly as possible (specifically with Mono).
      
	- Support all platforms.  The code currently works on 32-bit and 64-bit
		Windows.  It's been tested on 32-bit Linux and Mac OS X (using Mono).
		It should work as 64-bit on those platforms.  We're also supporting
		both TWAIN_32.DLL and TWAINDSM.DLL on Windows, and we'll support both
		TWAIN.framework and a TWAINDSM.framework (whenever it gets created).
      
	- Virtualiaze all public functions so that developers can extended the
		class with a minimum of fuss.