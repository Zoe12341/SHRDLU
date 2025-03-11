**From CSC 390 with Jamie Macbeth**  
**Getting Started with SHRDLU**  
____

This document describes loading and running Terry Winograd’s SHRDLU program from semi-original Common Lisp source code. It assumes that you have already successfully installed the CLISP Lisp interpreter, and that clisp is in your system’s path so that you can run it from within a Terminal or Command Prompt.
### 1 Running SHRDLU
- Download SHRDLU.zip from Moodle and unpack the ZIP archive
- Start a Terminal or Command Prompt and change the working directory to the “SHRDLU” directory created when unpacking the ZIP archive (using the cd com-
mand).
- Type clisp and ENTER to start CLISP
- Evaluate the expression (load 'loader) to evaluate all expressions in the file called LOADER from the archive. This will load all of the other files needed, and will start SHRDLU. At this point, you should see a “READY” prompt. You can now enter commands and queries to SHRDLU (e.g. “Pick up a big red block.” “What is in the box?”)
- You can also provide LOADER as an argument to clisp by typing clisp -i LOADER at the Terminal or Command Prompt. This will (mostly) have the same effect as
clisp followed by (load 'loader) .
- Try entering commands from SHRDLU demonstration transcripts that can be found online (e.g. https://en.wikipedia.org/wiki/SHRDLU ). You’ll find that some of the commands from these well-known transcripts work, and some of them don’t.
- Currently the best way to exit SHRDLU is by terminating the read function which is waiting for your commands. Hit Ctrl-D. This will launch the debugger. Type :q and ENTER to exit the debugger.
- To restart SHRDLU in the same CLISP REPL, evaluate (initialstuff nil nil) at the REPL. initialstuff is an informal “start” function created when SHRDLU was converted to Common Lisp in the 1990s.
 
### 2 Running SHRDLU in Debug Mode
Your SHRDLU code has a debug mode which provides some useful information about SHRDLU’s parsing, understanding and response processes. To try it, do the following:
- Edit LOADER and “comment out” the line near the bottom that says (USERMODE) by putting a ; in front of it.
- Remove the ; in front of (DEBUGMODE) so that the debugmode function is called with LOADER is loaded.
- Load LOADER as before. Instead of “READY”, the prompt will say “You are now in a read-eval-print loop. Type ‘go’ to enter ready state.” Type “go” and ENTER, and you should get the “READY” prompt.
- Enter SHRDLU commands as before. You should see additional information about SHRDLU’s parses, and about the MicroPlanner “theorem” structures (containing THAND , THGOAL , THFIND , etc.) which it generates and “proves” to carry out the
commands.

### 3 Tracing
You can see even more of SHRDLU’s internals by performing tracing on certain functions. Try starting SHRDLU in debug mode. Before typing “go” at the >>> prompt, enter (trace thval) . Then when you enter a SHRDLU command, you will see lines cor-
responding to each call to THVAL, which is the MicroPlanner theorem evaluation function. You will see the arguments to THVAL, which are MicroPlanner theorems that it will attempt to “prove” to execute the command, and when THVAL returns, you will also see what value was returned by the theorem evaluation (e.g. Trace: THVAL ==> (:B6) or Trace: THVAL ==> (0 300 700) ). Were you curious about SHRDLU’s definition of
“big?”. Ask SHRDLU to pick up a big red block with tracing of THVAL on.
