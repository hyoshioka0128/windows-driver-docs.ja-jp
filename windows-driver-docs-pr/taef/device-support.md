---
title: デバイスのサポート
description: デバイスのサポート
ms.assetid: 41316BB1-0AE0-4100-AE7B-0014FE9FD0E7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fef842911670299c4df585aed6a799023bcabcd6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341180"
---
# <a name="device-support"></a>デバイスのサポート


テスト自動化は、デバイスまたはテスト リソースの存在に依存する場合は、TestResourceExample の例を参照し、デバイス サポートを利用または TAEF で使用可能なリソースのサポートをテストする方法に従います。 TAEF と TAEF の基本的な実行を続行する前に使用して基本的なテストを作成する方法を理解していることを確認してください。

## <a name="span-idauthoringfordevicesupport-sourcesfilespanspan-idauthoringfordevicesupport-sourcesfilespanspan-idauthoringfordevicesupport-sourcesfilespanauthoring-for-device-support---sources-file"></a><span id="Authoring_for_device_support_-_Sources_file"></span><span id="authoring_for_device_support_-_sources_file"></span><span id="AUTHORING_FOR_DEVICE_SUPPORT_-_SOURCES_FILE"></span>デバイスのサポート - ソース ファイルの作成


Te.Common.lib が TAEF でテストを作成するために必要なその他のライブラリだけでなく必要です。

## <a name="span-idauthoringfordevicesupport-testresourcedefinitionspanspan-idauthoringfordevicesupport-testresourcedefinitionspanspan-idauthoringfordevicesupport-testresourcedefinitionspanauthoring-for-device-support---test-resource-definition"></a><span id="Authoring_for_device_support_-_Test_Resource_definition"></span><span id="authoring_for_device_support_-_test_resource_definition"></span><span id="AUTHORING_FOR_DEVICE_SUPPORT_-_TEST_RESOURCE_DEFINITION"></span>デバイスのサポート - テスト リソース定義の作成


ユーザーは、独自のテスト リソース (デバイス) の定義を作成する責任を負います。 これを行うには、ITestResource を実装する必要があります。 ITestResource では、ITestResource.h パブリッシュされたヘッダー ファイルで定義されており、次のようになります。

```cpp
namespace WEX { namespace TestExecution
{
    namespace TestResourceProperty
    {
        // the following are reserved and must have properties for any TestResource definition
        static const wchar_t c_szName[] = L"Name";
        static const wchar_t c_szId[] = L"Id";
        static const wchar_t c_szGuid[] = L"GUID";
        static const wchar_t c_szType[] = L"Type";
    }

    struct __declspec(novtable) __declspec(uuid("79098e4c-b78d-434b-854d-2b59f5c4acc5")) ITestResource : public IUnknown
    {
    public:
        virtual HRESULT STDMETHODCALLTYPE GetGuid(GUID* pGuid) = 0;
        virtual HRESULT STDMETHODCALLTYPE SetGuid(GUID guid) = 0;
        virtual HRESULT STDMETHODCALLTYPE GetValue(BSTR name, BSTR* pValue) = 0;
        virtual HRESULT STDMETHODCALLTYPE SetValue(BSTR name, BSTR value) = 0;
    };
} /*namespace TestExecution*/ } /*namespace WEX*/
```

この例では、クラス MyTestResource は ITestResource COM インターフェイスを実装します。 ITestResource.h で定義されている「必要がある」プロパティの一覧を検索することもされます。 GetGuid(..) と名前、Id および GetValue(...) を使用して、リソースの種類を使用して、テスト リソースの GUID を取得することができます。これのいずれかが不足している場合 TestResource、TAEF は consisder で無効であるし、その情報を保持しないようにします。(詳しくは、以下の「のリソース リストの作成」セクションを参照してください。)

## <a name="span-idauthoringfordevicesupport-specifyingresourcedependentmetadataspanspan-idauthoringfordevicesupport-specifyingresourcedependentmetadataspanspan-idauthoringfordevicesupport-specifyingresourcedependentmetadataspanauthoring-for-device-support---specifying-resource-dependent-metadata"></a><span id="Authoring_for_device_support_-_Specifying_resource_dependent_metadata"></span><span id="authoring_for_device_support_-_specifying_resource_dependent_metadata"></span><span id="AUTHORING_FOR_DEVICE_SUPPORT_-_SPECIFYING_RESOURCE_DEPENDENT_METADATA"></span>デバイスのサポートの作成 - リソースの依存のメタデータを指定します。


テスト モジュールにテスト リソースの依存のテスト方法、モジュール レベルのメタデータ プロパティがあることを指定するために **' TestResourceDependent"** 設定する必要があります"true"にします。 プロパティは、これらのクラスのすべてのテスト メソッドと、test モジュールのすべてのクラスによって継承を取得します。 テスト リソース依存モジュールのテスト メソッドのいずれかの場合にする必要があります明示的に再設定を false にメタデータ値。 テスト リソースの"Id"や"Type"を使用して選択クエリの指定のすべてのテストのリソースに依存するその他のテスト メソッドする必要があります。

ここで、リソース一覧の例とどのようないくつかの簡単なサンプル"ResourceSelection"をそれぞれの意味します。

-   "@Id='HD\*'":"HD"で始まる Id を使用して各リソースに一致
-   "@Type= 'PCI'":"PCI"の種類の各リソースに一致
-   "@Id='PCI\*' OR @Id='HD\*'":"PCI"の先頭または"HD"で始まる、各リソースに一致
-   "@Type= 'PCI' と@id='\*37'":「37」で終わる名前を持つ種類"PCI"のいずれかの各リソースに一致

コード例では、このようになります。

```cpp
BEGIN_MODULE()
    MODULE_PROPERTY(L"TestResourceDependent", L"true")
END_MODULE()

    class TestResourceExample
    {
        TEST_CLASS(TestResourceExample);

        BEGIN_TEST_METHOD(NoTestResourceTest)
            TEST_METHOD_PROPERTY(L"TestResourceDependent", L"false")
        END_TEST_METHOD()

        BEGIN_TEST_METHOD(OneHDAudioTest)
            TEST_METHOD_PROPERTY(L"ResourceSelection", L"@Id='HD*'")
        END_TEST_METHOD()

        ...

        BEGIN_TEST_METHOD(HDorPCITest)
            TEST_METHOD_PROPERTY(L"ResourceSelection", L"@Id='PCI*' OR @Id='HD*'")
        END_TEST_METHOD()
        ...
    };
```

上記の例では、モジュールが"TestResourceDependent"としてマークされていることがわかります。 NoTestResourceTest は"false"に"TestRssourceDependent"メタデータを設定して、テスト リソースに依存しないとして明示的にマークします。 その他のすべてのテスト メソッドの実行中の関心のあるテスト リソースの選択条件を指定します。

選択条件の文法では、commandline 選択クエリ文法 TAEF の使用によく似ています。 ただし、リソースの選択の場合は種類と Id をリソースの使用に制限します。 リソース Id は、文字列であるため、単一引用符で囲む必要があります。 ワイルドカード文字を使用することができます"\*「または」?"、Id 値の指定で。 OneHDAudioTest で、上記の例では、リソースの選択は、任意のリソース Id が 'HD' を開始する位置に一致するものを指定します。 同様に、HDorPCITest の場合、リソースの選択は任意のリソース Id が 'HD' で始まるか、'PCI' で始まるを一致します。 注意することが重要と扱わリソースの選択は、大文字小文字を区別には、'pci' と、'Pci'、'PCI' すべてになります。

リソースの選択に基づいて、TAEF は再テスト レベルの設定とテスト メソッドやメソッドを呼び出すクリーンアップ (指定されている) 場合 1 回の選択に一致するテスト リソースごとにします。 次のセクションでは、リソースの一覧を指定し、TAEF に提供する方法と、テスト メソッドを使用して、次のセクション内のリソースを取得する方法の詳細についてを説明します。

## <a name="span-idauthoringfordevicesupport-buildingtheresourcelistspanspan-idauthoringfordevicesupport-buildingtheresourcelistspanspan-idauthoringfordevicesupport-buildingtheresourcelistspanauthoring-for-device-support---building-the-resource-list"></a><span id="Authoring_for_device_support_-_Building_the_resource_list"></span><span id="authoring_for_device_support_-_building_the_resource_list"></span><span id="AUTHORING_FOR_DEVICE_SUPPORT_-_BUILDING_THE_RESOURCE_LIST"></span>デバイスのサポートの作成 - リソースのリストの作成


TAEF に TestResourceDependent テスト モジュールが検出されると、すぐに検索および BuildResourceList dll エクスポート メソッドを呼び出します。 ユーザーが、新しいテスト リソースを作成してで BuildResourceList をパラメーターとして渡されるインターフェイスに追加 BuildResourceList の実装です。 この例では、このメソッドの実装を見てをみましょう。

```cpp
using namespace WEX::TestExecution;
HRESULT __cdecl BuildResourceList(ResourceList& resourceList)
{
    Log::Comment(L"In BuildResourceList");

    GUID myGuid;
    VERIFY_SUCCEEDED(::CoCreateGuid(&myGuid));

    CComPtr<ITestResource> spTestResource;
    spTestResource.Attach(new MyTestResource(L"HDAudio1", L"HDAudio-deviceid-1", myGuid, L"HD"));
    resourceList.Add(spTestResource);

    spTestResource.Attach(new MyTestResource(L"HDAudio2", L"HDAudio-deviceid-2", myGuid, L"HD"));
    resourceList.Add(spTestResource);

    spTestResource.Attach(new MyTestResource(L"PCI1", L"PCI-deviceid-1", myGuid, L"PCI"));
    resourceList.Add(spTestResource);

    spTestResource.Attach(new MyTestResource(L"PCI2", L"PCI-deviceid-2", myGuid, L"PCI"));
    resourceList.Add(spTestResource);

    spTestResource.Attach(new MyTestResource(L"PCI3", L"PCI-deviceid-3", myGuid, L"PCI"));
    resourceList.Add(spTestResource);

    return S_OK;
}
```

BuildResourceList は、そのパラメーターとして WEX::TestExecution::ResourceList への参照を受け取ります。 ResourceList は ResourceList.h パブリッシュされたヘッダー ファイルで定義されます。 ユーザーで、ResourceList を add (...) メソッドを使用して、すべてのテスト リソースを検出または TAEF を管理および操作の作成を追加できます。 上記の例では、このようなテストの 5 つのリソースを追加します。

テスト リソースを追加するのには、リソースの"Name"、"Id"、"Type"または GUID を返すが失敗した場合、Add メソッドは失敗します。

ResourceList が使用して管理するテスト モジュールでの有効期間は、すべてのテスト メソッドとクリーンアップ メソッドが完了するまで実行します。 BuildResourceList 失敗 HRESULT 値を返す場合、実行することがなくブロックとしてテスト モジュール内のすべてのリソース依存のテスト メソッドが記録されます。 すべての非テスト リソースに関係なく実行されます。

BuildResourceList はテスト モジュールで他のメソッドの前に呼び出されます。 リソースの一覧を (BuildResourceList) で構築後"ResourceSelection"メタデータを使用して、リソースの一覧で使用可能なリソースを一致させる。 一致が見つかった場合 (モジュール、クラス、テストの順序) のすべてのセットアップ方法は、テスト メソッド自体で後に呼び出されます。 テスト レベルのクリーンアップ メソッドは、各テストの呼び出しの後に呼び出されます。

バック グラウンドでは、TAEF は、リソースの選択が適用される ResourceList を保持します。 たとえば、OneHDAudioTest テスト メソッドでは、テスト リソース Id「HDAudio deviceid 1」と「HDAudio deviceid 2」は両方と一致する 'HD\*' のこれらの各テスト メソッドによって再呼び出さ TAEF で (1 回のそれぞれ) とします。 テストの各呼び出しに関連付けられている暗黙のインデックスもあります。 表示されます、&lt;名前空間修飾子&gt;OneHDAudioTest\#0 と&lt;名前空間修飾子&gt;OneHDAudioTest\#1、2 つの呼び出しとして。

## <a name="span-idauthoringfordevicesupport-retrievingthedeviceinatestmethodspanspan-idauthoringfordevicesupport-retrievingthedeviceinatestmethodspanspan-idauthoringfordevicesupport-retrievingthedeviceinatestmethodspanauthoring-for-device-support---retrieving-the-device-in-a-test-method"></a><span id="Authoring_for_device_support_-_Retrieving_the_device_in_a_test_method"></span><span id="authoring_for_device_support_-_retrieving_the_device_in_a_test_method"></span><span id="AUTHORING_FOR_DEVICE_SUPPORT_-_RETRIEVING_THE_DEVICE_IN_A_TEST_METHOD"></span>テスト メソッドでデバイスを取得する - デバイスのサポートの作成


前のセクションでは、モジュール、クラス、およびテスト メソッドのレベルで、必要なメタデータを追加する方法を説明しました。 カスタム テスト リソースを定義する方法と BuildResourceList の実装で ResourceList に追加する方法にも注目します。 これに続く次の部分では、テスト メソッド内のリソースを取得しています。 この例では、簡単なテスト メソッドのいずれかを見てをみましょう。

```cpp
1   void TestResourceExample::OneHDAudioTest()
2   {
3       Log::Comment(L"In HD audio test");
4       size_t count = Resources::Count();
5       size_t index = 0;
6       VERIFY_ARE_EQUAL(count, (index + 1));
7
8       CComPtr<ITestResource> spTestResource;
9       VERIFY_SUCCEEDED(Resources::Item(index, &spTestResource));
10
11      // Get Resource Id
12      CComBSTR value;
13      VERIFY_SUCCEEDED(spTestResource->GetValue(CComBSTR(TestResourceProperty::c_szId), &value));
14      Log::Comment(L"Resource Id is " + String(value));
15  }
```

OneHDAudioTest では、リソースの選択は、リソース Id が 'HD' を開始する位置に 1 つのテスト リソースを選択します。 ResourceList.h でリソースが定義されている静的クラスは、テストの任意の特定の呼び出し中に使用できる実際のリソースと同様に、数を取得するための Api を提供します。 この場合、行 4、9、および上記の例では 13 に示すように、リソース:: Count() は現在、テスト メソッドの呼び出し時に使用可能なテスト リソースの数のカウントを提供します。 このテスト メソッドで 1 があります。 TAEF (Verify.h) で利用できることを確認マクロを使用して、この値を確認できます。 ご存知のと、例外ベース TAEF テストで検証呼び出しのいずれかが失敗した場合、その時点で、実行が終了し、テスト メソッドは、失敗としてマークされます。

[次へ] を使用して、Resources::Item(...)API と、テスト リソースを取得する (この場合、呼び出し中に 1 つだけのリソースを利用できる、ためインデックスは必ず 0) のリソースを取得する位置のインデックスを渡すことです。 さらに、テスト メソッドは、そのをテストするため、必要な取得したテスト リソースを使用します。

すべてのテスト メソッドは、同じ基本原則に従っています。 例をより深く理解するためにで、他のテスト メソッドを見てに設定します。

## <a name="span-idexecutingatestresourcedependenttestmodulespanspan-idexecutingatestresourcedependenttestmodulespanspan-idexecutingatestresourcedependenttestmodulespanexecuting-a-test-resource-dependent-test-module"></a><span id="Executing_a_test_resource_dependent_test_module"></span><span id="executing_a_test_resource_dependent_test_module"></span><span id="EXECUTING_A_TEST_RESOURCE_DEPENDENT_TEST_MODULE"></span>テスト リソース依存テスト モジュールの実行


テスト リソースは、ここで作成し、ビルドに依存するテスト、TAEF を使用してを実行することができますようになりました。 注意する重要な点は、TestResourceDependent テストが実行された inproc にすることができますのみです。 つまり、明示的に指定しない場合でも **"/inproc"** スイッチ、それが追加されますで TAEF テスト リソースの依存のテスト モジュールを検出するようになります。 特定の TAEF 実行におけるテストの 1 つだけのモジュールからのテストを実行できますご存知のように、ときに、"/inproc"スイッチが存在します。 つまり、test モジュールが依存するリソースの場合、commandline では、複数のテスト モジュールは指定できません。

実際に、テスト モジュール内のすべてのテストを実行、単純に実行できます。

``` syntax
te Examples\Cpp.TestResource.Example.dll
```

実際には、テスト メソッドを実行することがなくすべてのテスト メソッドの呼び出しと、データおよびメタデータの組み合わせの一覧を取得する便利な方法は、使用することです。 **/listproperties**コマンドラインに切り替えます。 出力を見ていきましょう。

``` syntax
te Examples\Cpp.TestResource.Example.dll /listproperties

Test Authoring and Execution Framework v2.9.3k for x86
In BuildResourceList
Verify: SUCCEEDED(::CoCreateGuid(&myGuid))

        f:\toolsdev.binaries.x86chk\WexTest\CuE\TestExecution\Examples\Cpp.TestResource.Example.dll
                Property[TestResourceDependent] = true

            WEX::TestExecution::Examples::TestResourceExample
                WEX::TestExecution::Examples::TestResourceExample::NoTestResourceTest
                        Property[TestResourceDependent] = false

                WEX::TestExecution::Examples::TestResourceExample::OneHDAudioTest#0
                        Property[ResourceSelection] = @Id='HD*' 
                
                            Resource#0
                                Id = HDAudio-deviceid-1
                                Name = HDAudio1
                                Type = HD

                WEX::TestExecution::Examples::TestResourceExample::OneHDAudioTest#1
                        Property[ResourceSelection] = @Id='HD*'
                        
                            Resource#0
                                Id = HDAudio-deviceid-2
                                Name = HDAudio2
                                Type = HD

                WEX::TestExecution::Examples::TestResourceExample::OnePCIDeviceTest#0
                        Property[ResourceSelection] = @Id='PCI*'
                        
                            Resource#0
                                Id = PCI-deviceid-1
                                Name = PCI1
                                Type = PCI

                WEX::TestExecution::Examples::TestResourceExample::OnePCIDeviceTest#1
                        Property[ResourceSelection] = @Id='PCI*'
                        
                            Resource#0
                                Id = PCI-deviceid-2
                                Name = PCI2
                                Type = PCI

                WEX::TestExecution::Examples::TestResourceExample::OnePCIDeviceTest#2
                         Property[ResourceSelection] = @Id='PCI*'
                        
                            Resource#0
                                Id = PCI-deviceid-3
                                Name = PCI3
                                Type = PCI

                WEX::TestExecution::Examples::TestResourceExample::HDorPCITest#0
                        Property[ResourceSelection] = @Id='PCI*' OR @Id='HD*'
                        
                            Resource#0
                                Id = HDAudio-deviceid-1
                                Name = HDAudio1
                                Type = HD

                WEX::TestExecution::Examples::TestResourceExample::HDorPCITest#1
                         Property[ResourceSelection] = @Id='PCI*' OR @Id='HD*'
                        
                            Resource#0
                                Id = HDAudio-deviceid-2
                                Name = HDAudio2
                                Type = HD

                WEX::TestExecution::Examples::TestResourceExample::HDorPCITest#2
                         Property[ResourceSelection] = @Id='PCI*' OR @Id='HD*'
                        
                            Resource#0
                                Id = PCI-deviceid-1
                                Name = PCI1
                                Type = PCI

                WEX::TestExecution::Examples::TestResourceExample::HDorPCITest#3
                         Property[ResourceSelection] = @Id='PCI*' OR @Id='HD*'
                        
                            Resource#0
                                Id = PCI-deviceid-2
                                Name = PCI2
                                Type = PCI

                WEX::TestExecution::Examples::TestResourceExample::HDorPCITest#4
                         Property[ResourceSelection] = @Id='PCI*' OR @Id='HD*'
                        
                            Resource#0
                                Id = PCI-deviceid-3
                                Name = PCI3
                                Type = PCI

                WEX::TestExecution::Examples::TestResourceExample::PCI1AudioTest #0
                         Property[ResourceSelection] = @Id='PCI*' AND @Id='*1'
                        
                            Resource#0
                                Id = PCI-deviceid-1
                                Name = PCI1
                                Type = PCI
```

暗黙のインデックスは depent テスト リソースの呼び出しごとにテスト メソッドの名前に追加取得メソッドをテストします。 その後で使用できる順序でテスト メソッドで使用できるすべてのリソースの一覧で、ResourceSelection プロパティが表示されます。 HDAudioHDAudioPCITest の 3 つ目の呼び出しが発生した場合など (HDAudioHDAudioPCITest\#2)、HDAudio-deviceid-1 は Resources::Item(...) でインデックス 0 位置にある使用可能なリソースになります。

Commandline 選択範囲の TAEF で使用できるクエリ言語を使用して、関心のあるどのテスト呼び出しに関する具体的なことができます。 テスト リソース「PCI deviceid 3」が使用可能なテスト メソッドのすべての呼び出しを選択する例では、選択条件を使用できます。

``` syntax
te Examples\Cpp.TestResource.Example.dll /list
          /select:"@Resource:Id='PCI-deviceid-3'"

Test Authoring and Execution Framework v2.9.3k for x86
In BuildResourceList
Verify: SUCCEEDED(::CoCreateGuid(&myGuid))

        f: \Examples\Cpp.TestResource.Example.dll
            WEX::TestExecution::Examples::TestResourceExample
                WEX::TestExecution::Examples::TestResourceExample::OnePCIDeviceTest#2
                WEX::TestExecution::Examples::TestResourceExample::HDorPCITest#4
```

同様に、名前 (注テスト メソッドの末尾に付加された呼び出しのインデックスと共に完全修飾名では)、特定のテスト メソッドを選択することができますように使用する選択クエリ。

``` syntax
te Examples\Cpp.TestResource.Example.dll /name:*OneHDAudioTest#1
Test Authoring and Execution Framework v2.2 Build 6.1.7689.0 (release.091218-1251) for x86

Discovered a test resource dependent test module. Assuming /InProc execution.

In BuildResourceList
Verify: SUCCEEDED(::CoCreateGuid(&myGuid))

StartGroup: WEX::TestExecution::Examples::TestResourceExample::OneHDAudioTest#1
In HD audio test
Verify: AreEqual(count, (index + 1))
Verify: SUCCEEDED(Resources::Item(index, &spTestResource))
Verify: SUCCEEDED(spTestResource->GetValue(CComBSTR(TestResourceProperty::c_szId), &value))
Resource Id is HDAudio-deviceid-2
WEX::TestExecution::Examples::TestResourceExample::OneHDAudioTest#1 [Passed]

Summary: Total=1, Passed=1, Failed=0, Blocked=0, Not Run=0, Skipped=0
```

上記の例の 3 番目の行に警告追加暗黙的な inproc に注意してください。 上記の選択クエリには、選択クエリと同じ効果が必要がある:**選択/:"@Name='\*OneHDAudio\*' と@Resource:Index= 1"** します。 名または型 (または前の例の Id) を使用してリソースを選択することもできます。 たとえば、**選択/:"@Name='\*PCIHDAudioTest\*' と@Resource:Name= 'PCI3'"** メソッド PCIHDAudioTest テスト選択は\#4 および PCIHDAudioTest\#5。

これらとコマンド プロンプトでその他の選択クエリを試すについては、リーダーの演習として残しています。

 

 





