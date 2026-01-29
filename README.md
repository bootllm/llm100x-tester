# BCS100X Tester

BCS100X 课程自动化测试工具。

## 方式一：源码运行

```bash
# 克隆项目
git clone https://github.com/bootcs-cn/bcs100x-tester
cd bcs100x-tester

# 编译
go build .

# 测试
./bcs100x-tester -s hello -d ~/cs50/hello
./bcs100x-tester --list
```

**环境依赖：** Go 1.24+, clang, python3, sqlite3

## 方式二：Docker 镜像

```bash
# 使用 Docker Hub 镜像（推荐）
cd ~/my-solution  # 进入你的代码目录
docker pull bootcs/bcs100x-tester
docker run --rm -v "$(pwd):/workspace" bootcs/bcs100x-tester -s hello -d /workspace/hello

# 或本地构建镜像
git clone https://github.com/bootcs-cn/bcs100x-tester
cd bcs100x-tester
docker build -t bootcs/bcs100x-tester:local .

# 切换到代码目录测试
cd ~/my-solution/hello
docker run --rm -v "$(pwd)/..:/workspace" bootcs/bcs100x-tester:local -s hello -d /workspace/hello
```

**建议：** 创建包装脚本简化使用

```bash
# 在代码根目录创建 test.sh
cat > test.sh << 'EOF'
#!/bin/bash
# 用法: ./test.sh hello
STAGE=${1:-hello}
docker run --rm -v "$(pwd):/workspace" bootcs/bcs100x-tester -s "$STAGE" -d "/workspace/$STAGE"
EOF

chmod +x test.sh
./test.sh hello      # 测试 hello
./test.sh caesar     # 测试 caesar
```

**说明：** `-v` 挂载代码目录到容器，需要可写权限用于编译。

## License

MIT
