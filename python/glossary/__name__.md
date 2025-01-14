Python has a global variable `__name__` which is set to `"__main__"` if the script being run directly, or set to the name of the module (its filename) if it is just being automatically executed as part of an import statement.

```python hlt:6
# ...

def main():
    # Implemention...

if __name__ == "__main__":
    main()
```


