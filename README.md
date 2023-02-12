
### 目标  
1. 从ubpf库剥离出一个干净的可移植的libebpf  
- 有清晰的API，通过基本测试  
- 通过全部单元测试  
- 补充arm32位JIT  

2. 研究形式化验证，思考如何针对这个库进行验证  
- 从Linux kernel复制已经验证了的，用JitterBug的方法验证  
- 重新针对当前实现进行形式化验证  

## 进度Milestone
1. （done）复制文件，重命名  
ubpf.h -> libebpf.h
ebpf.h -> ebpf_inst.h
ubpf_int.h -> ebpf_vm.h
2. (done) libebpf make  
3. test.c基础测试  
4. 工具链测试  
5. (done) 单元测试  

### 编译项目  
```
make 
make test
# 或者单独测
make smoke_test
make unit_test
```
调试项目:



### 测试项目  
1. Smoke Test

2. 单元测试  
```
# 根目录下
pip3 install -r test/requirements.txt 
nosetests3 -v
```

运行结果：  
> Ran 942 tests in 1.243s
> OK (SKIP=668)

## Notes  
1. 查看静态库的函数  
nm -gC bin/libebpf.a  
或者：
readelf -sW bin/libebpf.a | awk '$4 == "FUNC"' | c++filt

2. gcc参数顺序  
最好把src放在第一个参数，中间放flags，不然会src和ldflags混在一起报错。  
