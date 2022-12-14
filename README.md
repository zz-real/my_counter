# 增加一个自然数
1. 在本教程中，您将编写一个程序来创建单个参与者并提供一些基本函数来增加计数器并说明值的持久性。

2. 在本教程中，演员被命名为Counter。该程序使用该currentValue变量包含一个自然数，该自然数表示计数器的当前值。该程序支持以下函数调用：

increment函数调用更新当前值，将其递增 1（无返回值）。

函数调用查询并返回计数器的get当前值。

函数调用将set当前值更新为您指定为参数的任意数值。

3. 本教程提供了一个简单示例，说明如何通过调用已部署容器上的函数来增加计数器。通过多次调用函数递增和查询计数器值，您可以验证变量状态（即两次调用之间的变量值）是否保持不变。

# 之前
在开始本教程之前，请验证以下内容：

您已按照下载和安装中的说明下载并安装了 SDK 包。

您已停止计算机上运行的任何本地容器执行环境。

完成本教程大约需要 20 分钟。

# 创建一个新
要为本教程创建一个新的项目目录：

1. 如果您还没有打开终端外壳，请在本地计算机上打开终端外壳。

2. 更改为您用于 Internet 计算机项目的文件夹（如果您正在使用一个文件夹）。

3. 通过运行以下命令创建一个新项目：

dfx new my_counter --no-frontend

该命令为您的项目创建一个新my_counter项目。

4. 通过运行以下命令切换到您的项目目录：

cd my_counter

# 修改默认
您已经看到创建新项目会将默认dfx.json配置文件添加到项目目录中。在本教程中，您将修改默认设置，为项目中的主程序使用不同的名称。

修改dfx.json配置文件：

1. dfx.json在文本编辑器中打开配置文件并将默认main设置从更改main.mo为increment_counter.mo。

例如：

"main": "src/my_counter/increment_counter.mo",

对于本教程，将源文件的名称从更改main.mo为increment_counter.mo简单说明dfx.json配置文件中的设置如何确定要编译的源文件。

在更复杂的 dapp 中，您可能有多个具有依赖关系的源文件，您需要使用dfx.json配置文件中的设置来管理这些源文件。dfx.json在这样的场景中——在你的文件中定义了多个容器和程序——同时命名多个文件main.mo可能会让人感到困惑。

您可以保留其余的默认设置。

2. 保存更改并关闭dfx.json文件以继续。

3. 通过运行以下命令将源代码目录中的主程序文件的名称更改为与配置文件src中指定的名称匹配dfx.json

mv src/my_counter/main.mo src/my_counter/increment_counter.mo

# 修改默认
到目前为止，您只更改了项目的主程序的名称。下一步是修改src/my_counter/increment_counter.mo文件中的代码以定义一个名为Counter并实现increment、get和set函数的参与者。

修改默认模板源代码：

1. 如果需要，请检查您是否仍在项目目录中。

2. 在文本编辑器中打开src/my_counter/increment_counter.mo文件并删除现有内容。

3. 将此代码复制并粘贴到increment_counter.mo文件中。

让我们仔细看看这个示例程序：

您可以看到，currentValue此示例中的变量声明包含stable指示状态的关键字——可以设置、递增和检索的值——持续存在。

该关键字确保程序升级时变量的值不变。

变量的声明currentValue还指定其类型为自然数 ( Nat)。

该程序包括两个公共更新方法 -increment和set函数 - 和一个查询方法 -get函数。

有关稳定变量和灵活变量的更多信息，请参阅《 Motoko 编程语言指南》中的稳定变量和升级方法。

有关查询和更新之间差异的更多信息，请参阅容器中的查询和更新方法包括程序和状态。

4. 保存更改并关闭文件以继续。

# 启动本地容器执行
在构建my_counter项目之前，您需要连接到模拟 Internet Computer 区块链的本地容器执行环境或 Internet Computer 区块链主网。

启动本地容器执行环境需要一个dfx.json文件，因此您应该确保您位于项目的根目录中。对于本教程，您应该有两个独立的终端 shell，以便您可以在一个终端中启动和查看网络操作并在另一个终端中管理您的项目。

启动本地容器执行环境：

1. 在本地计算机上打开一个新的终端窗口或选项卡。

2. 如有必要，导航到项目的根目录。

您现在应该打开两个终端。

您应该将项目目录作为当前工作目录。

3. 通过运行以下命令在您的计算机上启动本地容器执行环境：

dfx start --background

启动本地容器执行环境后，终端会显示有关网络操作的消息。

4. 让显示网络操作的终端保持打开状态，然后将注意力转移到创建新项目的原始终端。

# 注册、构建和部署
连接到在您的开发环境中运行的本地容器执行环境后，您可以在本地注册、构建和部署您的 dapp。

要在本地部署 dapp：

1. 如果需要，请检查您是否仍在项目的根目录中。

2. 通过运行以下命令注册、构建和部署您的 dapp：

dfx deploy

dfx deploy命令输出显示有关它执行的操作的信息。

# 在已部署的
成功部署容器后，您可以模拟最终用户调用容器提供的方法。在本教程中，您将调用get查询计数器值的increment方法、每次调用时递增计数器的set方法以及传递参数以将计数器更新为您指定的任意值的方法。

要在已部署的容器上测试调用方法：

1. 运行以下命令调用该函数，该函数读取已部署容器上变量get的当前值：currentValue

dfx canister call my_counter get

该命令将currentValue变量的当前值返回为零：

(0 : nat)

2. 运行以下命令以调用increment函数以将currentValue已部署容器上的变量值加一：

dfx canister call my_counter increment

这个命令增加变量的值——改变它的状态——但不返回结果。

3. 重新运行以下命令以获取已currentValue部署容器上变量的当前值：

dfx canister call my_counter get

该命令将currentValue变量的更新值返回为 1：

(1 : nat)

4. 运行其他命令来尝试调用其他方法和使用不同的值。

例如，尝试类似以下的命令来设置和返回计数器值：

dfx canister call my_counter set '(987)'
dfx canister call my_counter get

这将返回currentValue987 的更新值。运行附加命令

dfx canister call my_counter increment
dfx canister call my_counter get

返回 988 的增量currentValue。

5. 使用坦率的 ui 测试您的代码。

要测试您的代码，请按照此处的说明进行操作。

# 停止本地容器执行
完成 dapp 试验后，您可以停止本地容器执行环境，使其不会继续在后台运行。

要停止本地容器执行环境：

1. 在显示网络操作的终端中，按 Control-C 可中断本地容器执行环境。

2. 通过运行以下命令停止本地容器执行环境：

dfx stop

# call 调用
1. dfx canister call my_counter_backend http_request '(record {body = blob ""; headers = vec {}; method = "GET"; url = "/"})'