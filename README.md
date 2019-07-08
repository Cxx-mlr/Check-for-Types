# Type Restrictor
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -  - - 
    by: Ksenia Milkand & Cxx
```cpp
#include <iostream>
#include <type_traits>

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

template <class element_0, class... element_rest>
struct _restrict_ {

	template <class type_0, class... type_rest>
	struct _access_to_ {

	template <class type_x0, class... type_xrest>
	constexpr static decltype(auto) process(type_x0 args0, type_xrest... arg_rest)
	{
		return [](auto... args)
		{
			static_assert(!(list <type_x0, type_rest...>::template contain <element_0, element_rest...>::value &&
						    list <decltype(args)...>::template contain <type_0, type_rest...>::value),
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
first version by Ksenia Milkand & Cxx - https://godbolt.org/z/-Rf0M9
