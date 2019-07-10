# Type Restrictor
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -  - - 
    by: Ksenia Milkand & Cxx
```cpp
#include <iostream>
#include <type_traits>

template <class type, class... types>
struct list
{
    private:
        template <class>
        struct identity {
        };

        template <class... types_>
        struct identities : identity <types_>... {
        };

    public:
        template <class element, class... elements>
        struct contain
        {
            constexpr static bool value = std::is_base_of <identity <type> , identities <element, elements...>>::value || 
                                         (std::is_base_of <identity <types>, identities <element, elements...>>::value || ...);
        };
};

template <class element_0, class... element_rest>
struct _restrict_
{
    template <class type_0, class... type_rest>
    struct _access_to_ {
    
        template <class type_x0, class... type_rest>
        constexpr static decltype(auto) process(type_x0 args0, type_rest... arg_rest)
        {
            return [](auto... args)
            {
                    static_assert(!(list <type_x0, type_rest...>::template contain <element_0, element_rest...>::value &&
                                    list <    decltype(args)...>::template contain <   type_0, type_rest   ...>::value),
                    "bad_type_access"
                    );

                puts("processing elements");
            };
        };
    };

    _restrict_() = delete;
};

#define as )(

int main() {
    using mode = _restrict_ <int>::_access_to_ <float, double>;
    //mode::process(int{} as float{}, double{}); //assert
    mode::process(char{} as float{}, double{});
    return 0;
}
```
first version by Ksenia Milkand & Cxx - https://godbolt.org/z/IMU6KX
