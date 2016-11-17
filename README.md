GMatrix
=======

**GMatrix** (originally GRPC Matrix) is a project to make the [Matrix Protocol](http://matrix.org) suitable for real-world applications.

It uses the same approach, but implements some things differently.

 - ProtoBuf and GRPC are used for the RPC calls and messages.
 - A compatibility layer is implemented for interop with standard Matrix implementations
 - Pluggable storage backends
 - Pluggable event callbacks, verification / validation, identity, conflict resolution (Applic)
 - Public-key identified clients, X.509 for permissions + verification on default
 - CAP Theorem: particular focus on availability and partition tolerance over consistency
 - Efficient backfill

The primary intent of this project is to re-imagine Matrix as a platform for data-sync of any kind by designing it with performance and throughput in mind. The current implementations are primarily designed for chat-rooms.

While some inter-op is planned, it is not a priority.

Pluggable Components
====================

All "pluggable" components support third-party implementations of features. This is accomplished by calling the modular implementations one of several ways:

 - Starting a sub-process with stdin as a GRPC channel.
 - Calling a GRPC service over standard HTTP/2.

Furthermore, pluggable components can be marked as "optional" or "required." This is important for conflict resolution / validation type components, where you may be interested in stopping the server from processing new messages without validation calls returning successfully.
