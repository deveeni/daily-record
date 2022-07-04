# React Hooks : useCallback() 어떻게 사용하는것인가


## Problem
### useEffect 사용중에 deps에 함수를 넘기는 경우, Javascript `함수동등성`에 의해 무한으로 호출됨

### 함수 동등성 (Function equality)
- Javascript 는 `함수`도 `object`로 여기기 때문에 `주소에 의한 참조 비교`가 발생한다. 
```
  const add1 = () => x + y;
  const add2 = () => x + y;
  add1 === add2 //false
```

이때문에, 아래와 같이 무한루프를 겪게 되었다. 
```
  ...
  const [keyword, setKeyword] = useState('test');
  const { handleChange } = props;

  useEffect(() => { 
      handleChange(); // -> 계속~ 호출 됨 (Infinite Loop)
  }, [keyword, handleChange]);
  ...
```

## Solve
- 이럴때 `useCallback()` 을 사용하면된다.
- useCallback() 은 함수를 `memoization` 하기 위해 사용된다.
- 두번째 인자의 deps배열에 있는 값이 변경될 때까지 함수를 저장해 놓고, 재사용 할 수 있게 한다.

``` 
  const memoizationCallback = useCallback(func, [deps]);
```
