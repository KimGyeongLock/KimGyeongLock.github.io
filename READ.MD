1. jsmn 실행
    * `./cimin -i jsmn/testcases/crash.json -m "heap-buffer-overflow" -o reduced jsmn/jsondump`
2. libxml2 실행
    * `./cimin -i libxml2/testcases/crash.xml -m "SECV" -o reduced libxml2/xmllint --recover --postvalid -`
3. balance 실행
    * `./cimin -i balance/testcases/pass -m "" -o reduced balance/balance`
    * `./cimin -i balance/testcases/fail -m "" -o reduced balance/balance`
4. libpng 실행
    * `./cimin -i libpng/crash.png -m "use-of-uninitialized-value" -o reduced libpng/libpng/test_pngfix`
