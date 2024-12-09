# Go Race Condition in Concurrent Print with Mutex

This repository demonstrates a subtle race condition in a Go program that uses a mutex to protect shared access to standard output.  The program uses goroutines and a wait group for concurrent execution. Although it appears to be correctly synchronized, a close examination reveals the issue.

The `bug.go` file contains the buggy code. The `bugSolution.go` file shows how to correct the issue.

## Bug Description

The program aims to print numbers 0-9 in order using goroutines and a mutex. However, due to the way the goroutines and the mutex are handled, the output may be unpredictable and out of order.  This is because the goroutine closure captures the variable `i` by reference, leading to a race condition.