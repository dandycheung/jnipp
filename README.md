What is this?
=============

jnipp is a C++11 Java Native Interface wrapper supposed to make life easier.


Usage without generated classes
===============================

    Env::Scope scope(jni_env_pointer);
    LocalRef<String> str = String::create("Some String!");
    Method<String> String_toUpperCase("java/lang/String", "toUpperCase", "()Ljava/lang/String;");
    LocalRef<String> str_upper = String_toUpperCase(str);


Usage with generated classes
============================

use ./generate java.lang.String to generate the java class header file

    Env::Scope scope(jni_env_pointer);
    LocalRef<JavaLangString> str = String::create("Some String!");
    LocalRef<JavaLangString> str_upper = str->toUpperCase();


Runtime size and speed
======================

This library is designed to generate as close to manually written code as possible.
- All functions are inlined
- No additional reference counters
- No allocations
- the "test" sample produces a .dylib of 30kb

When using java class headers you need to use dead code stripping, for clang:
    clang source.cpp -fvisibility=hidden -fvisibility-inlines-hidden
    clang source.o -Wl,-dead_strip


TODO
====
- better tutorial
- clean up generate tool (own dir, .jar, output file name option etc.)
- Jni::Env should be a thread_local
