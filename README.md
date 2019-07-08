# Check-for-Types
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -  - - 
    by: Ksenia Milkand & Cxx
```cpp
template <class... element_rest>
struct list
{
    template <class... type_rest>
    class contain
    {
    private:
        template <class check_0, class... check_rest>
        struct _is_same_ {
            constexpr static bool value = (std::is_same <check_0, check_rest>::value || ...);
        };

    public:
        constexpr static bool value = (_is_same_ <type_rest, element_rest...>::value || ...);
            using type = typename std::common_type <type_rest...>::type;
        };
};

int main()
{
    if constexpr (list <int, int>::contain <float, int, float>::value)
        putchar('t');

    else
        putchar('f');
	
    return 0;
}
```
