---
title: WMI データ ソース
description: WMI データ ソース
ms.assetid: 1C9D0EEC-6542-4249-B7E0-CA3ED63FB120
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1e72d3a653f0b4235e954b00a607c9d05d7b789
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552135"
---
# <a name="wmi-data-source"></a>WMI データ ソース


TAEF の基本的な実行に精通していることを確認してください作成者テストが、このセクションに進む前に使用する方法。

## <a name="span-idbackgroundspanspan-idbackgroundspanspan-idbackgroundspanbackground"></a><span id="Background"></span><span id="background"></span><span id="BACKGROUND"></span>バック グラウンド


"WMI""Windows Management Instrumentation"の略です。 Common Information Model (CIM) を使用して、業界標準を表すシステムです。 Windows Management Instrumentation は、システムの管理情報にアクセスするための統一された方法を提供します。

## <a name="span-idhowdoesithelpmytestsspanspan-idhowdoesithelpmytestsspanspan-idhowdoesithelpmytestsspanhow-does-it-help-my-tests"></a><span id="How_does_it_help_my_tests_"></span><span id="how_does_it_help_my_tests_"></span><span id="HOW_DOES_IT_HELP_MY_TESTS_"></span>今回のテストをどのように役立つことでしょうか。


TAEF WMI データ ソースとして使用可能な WMI クエリのサポートを使用して、することができます、テストに前提条件を追加するだけでなく、テストを実行する前にテスト コンピューターで、リソースに関する情報を取得します。 いくつかの WMI を使用することもできますクエリの種類の例を次に示します。

-   チェック、マシンでテストが実行されている場合は、ラップトップし、ラップトップ コンピューターである場合にのみ、テストを実行します。
-   サービス パックが、テスト コンピューターにインストールされているし、テストを実行している場合にのみかどうかを確認します。
-   すべてのテスト コンピューターでローカルのハード ディスク ドライブとリムーバブル ドライブを取得し、各クエリに一致するドライブのテストを実行します。
-   テストの実行、テスト マシンがドメインではない場合にのみ参加している OR
-   テスト マシンがドメイン参加し、ドメイン名を取得する場合にのみ、テストを実行します。

願ってテストに WMI のデータ ソースを利用するには場所と方法についていくつかの考え方です。 TAEF テストを作成する際にこの WMI クエリのサポートを追加する方法を見てみましょう。

WMI のデータ ソースのテスト、テストを作成する必要がある唯一の特殊なメタデータは、「データ ソース」です。 DataSource 構文ように表示する必要があります。

```cpp
[DataSource("WMI:<WQL query>")]
```

または、ネイティブ コードで。

```cpp
TEST_METHOD_PROPERTY(L"DataSource", L"WMI:<WQL query>")]
```

データ ソースの値が始まるお気づきする必要があります"WMI:"このことは実際のデータ ソースは WMI クエリの結果に依存し、データ ドリブン テストからともテストを TAEF ことができます。 これは、現在 TAEF が WMI クエリの結果に依存するテスト - だけでなく、データ ドリブン テストするテストをサポートしていませんについて言及する良い機会になります。

次の質問は、探しているものの WQL クエリを記述する方法を当然ですか。 WQL クエリの構文が簡略化された SQL クエリとよく似ています。 提供されるクエリの非常に良好な例をいくつかある[https://msdn2.microsoft.com/library/aa394585(VS.85).aspxします。](https://msdn2.microsoft.com/library/aa394585(VS.85).aspx) 以下は例です。

<span id="SELECT_Description__DesktopInteract__ProcessId_FROM_Win32_Service_WHERE_Name__Themes_"></span><span id="select_description__desktopinteract__processid_from_win32_service_where_name__themes_"></span><span id="SELECT_DESCRIPTION__DESKTOPINTERACT__PROCESSID_FROM_WIN32_SERVICE_WHERE_NAME__THEMES_"></span>選択の説明、DesktopInteract、ProcessId Win32 から\_サービス名 = 'テーマ'  
「テーマ」サービスでの説明、DesktopInteract、ProcessId プロパティを使用するテストを行う予定が見つかったら、テストを実行します。

<span id="SELECT_Capabilities__CapabilityDescriptions_FROM_Win32_Printe"></span><span id="select_capabilities__capabilitydescriptions_from_win32_printe"></span><span id="SELECT_CAPABILITIES__CAPABILITYDESCRIPTIONS_FROM_WIN32_PRINTE"></span>機能、CapabilityDescriptions Win32 から\_プリンター  
このコンピューターに接続されている各プリンターのテストを実行します。 テストの各プリンターの機能と CapabilityDescriptions へのアクセスを許可します。

<span id="SELECT_Name__User__Location_FROM_Win32_StartupCommand"></span><span id="select_name__user__location_from_win32_startupcommand"></span><span id="SELECT_NAME__USER__LOCATION_FROM_WIN32_STARTUPCOMMAND"></span>SELECT Name, ユーザー、場所 Win32 から\_StartupCommand  
Windows の起動時に実行を取得する各プロセスのテストを実行します。 プロセスの名前が不明が配置されている (場所)、およびどのようなテストを使用する各プロセスのユーザーとして、プロセスが実行されます。

例については、.cs ファイルとヘッダー ファイルを開く例のようにも上記のドキュメントにあります。 一般に、過剰にシンプルな構文は次のとおりです。

```cpp
SELECT <comma separated properties> FROM <WMI Class name> [WHERE <add condition on some properties>]
```

Win32 の例を説明する\_サービス、Win32\_プリンターと Win32\_StartupCommand はすべての WMI クラスです。 ここで、テストの関心はどのような WMI クラスを調べることができます: [https://msdn2.microsoft.com/library/aa394554(VS.85).aspxします。](https://msdn2.microsoft.com/library/aa394554(VS.85).aspx)

TAEF では、システムのプロパティを取得することはできません。

シーンの背後にある TAEF は、クエリを実行し、結果を確認します。 少なくとも 1 つのオブジェクトが、クエリの結果として返された場合は、返された各オブジェクトのテストが実行されます。 WQL クエリがすべてのオブジェクトを返さない場合は、この情報を含むテストのブロックとしてログに記録を取得し、実行が次のテストに移ります。

チェックや、テストを作成する前に、クエリを確認する、アイデアのようし、は非常に単純なプロセスです。

-   実行の ダイアログ ボックスまたはコマンド プロンプトから"wbemtest.exe"を呼び出す
-   右上隅の [接続] ボタンをクリックします。
-   名前空間は必ず"ルート\\cimv2"右上隅の [接続] をもう一度クリックする前にします。
-   「[Iwbemservices]」の下"の Query"をクリックします。
-   「適用」 をクリックし、表示される編集ボックスに、クエリを入力します。

注: "IWbemService"には、クエリに役立つ可能性のあるいくつか他のオプションがあります。 たとえば、「クラスの列挙」を使用して、オプション ボタンを「再帰的な」に変更する際に役立つシステム上のすべての WMI クラスを参照してください。

## <a name="span-idretrievingpropertiesqueriedusingthewmiqueryspanspan-idretrievingpropertiesqueriedusingthewmiqueryspanspan-idretrievingpropertiesqueriedusingthewmiqueryspanretrieving-properties-queried-using-the-wmi-query"></a><span id="Retrieving_properties_queried_using_the_WMI_query"></span><span id="retrieving_properties_queried_using_the_wmi_query"></span><span id="RETRIEVING_PROPERTIES_QUERIED_USING_THE_WMI_QUERY"></span>WMI クエリを使用して照会するプロパティを取得します。


ここまででは、WMI クエリのテスト メソッドを考案する方法と、テストの作成中にメタデータとして適用する方法は把握しています。 また、クエリが wbemtest.exe を使用して有効であることを確認する方法を理解します。 今すぐ検索対象のプロパティ値を取得する方法を見てみましょう。

この情報を取得する方法の基礎は、データ ドリブン テストの値を取得するとよく似ています。 たとえば、マネージ コードでこれがようになります。

```cpp
1 namespace WEX.Examples
2 {
3     using Microsoft.VisualStudio.TestTools.UnitTesting;
4     using System;
5     using System.Collections;
6     using System.Data;
7     using WEX.Logging.Interop;
8     using WEX.TestExecution;
9
10    [TestClass]
11    public class CSharpWmiDataSourceExample
12    {
13        [TestMethod]
14        [DataSource("WMI:SELECT Description, DesktopInteract, ProcessId FROM Win32_Service WHERE Name=&#39;Themes&#39;")]
15        public void ThemesTest()
16        {
17            String description = (String)m_testContext.DataRow["Description"];
18            Boolean desktopInteract = (Boolean)m_testContext.DataRow["DesktopInteract"];
19            UInt32 processId = (UInt32)m_testContext.DataRow["ProcessId"];
20            Log.Comment("Themes service is running on process " + processId.ToString() + " with desktop interact set to "
                           + desktopInteract.ToString());
21            Log.Comment("Themes service description: " + description);
22        }
23        ...
24        public TestContext TestContext
25        {
26            get { return m_testContext; }
27            set { m_testContext = value; }
28        }
29
30        private TestContext m_testContext;
31    }
32}
```

上記の例では 24 ~ 30 の行は、管理対象のデータ ドリブン テストに必要なものにまったくです。 プライベートの TestContext プロパティを定義し、TAEF 適切な値を設定するためには、パブリック ゲッターとセッターを提供します。 プライベートの TestContext プロパティを使用すると、TAEF から取得した、WMI クエリ結果オブジェクトのプロパティのいずれかの現在の値を取得できます。

WMI のプロパティを取得するためのネイティブ コードでは、よく似ています。 ネイティブのデータ ドリブン テストを使用したようにプロパティ値を取得するのに TestData を使用します。 たとえば、既定のプリンターのプロパティを取得するためのテストについて考えてみましょう。 ヘッダー ファイルでこのテストが作成できるようになります。

```cpp
1        // Test on the default printer and its driver name
2        BEGIN_TEST_METHOD(DefaultPrinterTest)
3            TEST_METHOD_PROPERTY(L"DataSource",
              L"WMI:SELECT DriverName, DeviceId, LanguagesSupported FROM Win32_Printer WHERE Default = True")
4        END_TEST_METHOD()
```

これは、cpp ファイルで、取得コードは次のようになります。

```cpp
1     void WmiExample::DefaultPrinterTest()
2     {
3         String deviceId;
4         VERIFY_SUCCEEDED(TestData::TryGetValue(L"DeviceId", deviceId));
5
6         String driverName;
7         VERIFY_SUCCEEDED(TestData::TryGetValue(L"DriverName", driverName));
8
9         TestDataArray<unsigned int> languagesSupported;
10        VERIFY_SUCCEEDED(TestData::TryGetValue(L"LanguagesSupported", languagesSupported));
11
12        Log::Comment(L"The default driver is " + deviceId + L" which is a " + driverName);
13        size_t count = languagesSupported.GetSize();
14        for (size_t i = 0; i < count; i++)
15        {
16            Log::Comment(String().Format(L"Language supported: %d", languagesSupported[i]));
17        }
18    }
```

## <a name="span-idaccountingforpossiblenullpropertyvaluesspanspan-idaccountingforpossiblenullpropertyvaluesspanspan-idaccountingforpossiblenullpropertyvaluesspanaccounting-for-possible-null-property-values"></a><span id="Accounting_for_possible_NULL_property_values"></span><span id="accounting_for_possible_null_property_values"></span><span id="ACCOUNTING_FOR_POSSIBLE_NULL_PROPERTY_VALUES"></span>NULL プロパティ値の計算


留意するパートは、WMI クエリによって null 以外のプロパティが常に返すしないようにします。 返される WMI プロパティの値が"null"場合があります。 探しているプロパティは、一部のシナリオで"null"にできることと思われる場合のを確認の検証または使用を試みる前に。

管理対象のテスト コードなどの TestContext は DBNull 型のオブジェクトとして null 値を格納します。 することが予想されるオブジェクトの型に結果の値をキャストする前に DBNull 型の場合を確認する必要があります。 見てみましょう。

```cpp
1 namespace WEX.Examples
2 {
3     using Microsoft.VisualStudio.TestTools.UnitTesting;
4     using System;
5     using System.Collections;
6     using System.Data;
7     using WEX.Logging.Interop;
8     using WEX.TestExecution;
9
10    [TestClass]
11    public class CSharpWmiDataSourceExample
12    {
13        [TestMethod]
14        [DataSource("WMI:SELECT MaximumComponentLength, Availability, DeviceId, DriveType, Compressed
                         FROM Win32_LogicalDisk WHERE DriveType=2 Or DriveType=3")]
15        public void LogicalDiskTest()
16        {
17            UInt32 driveType = (UInt32)m_testContext.DataRow["DriveType"];
18            Log.Comment("DeviceId is " + m_testContext.DataRow["DeviceId"]);
19            Log.Comment("DriveType is " + driveType.ToString());
20
21            object nullCheckCompressed = m_testContext.DataRow["Compressed"];
22            Log.Comment("Compressed&#39;s type is: " + nullCheckCompressed.GetType().ToString());
23            if (nullCheckCompressed.GetType() == typeof(DBNull))
24            {
25                Log.Comment("Compressed is NULL");
26            }
27            else
28            {
29                Boolean compressed = (Boolean)nullCheckCompressed;
30                Log.Comment("Compressed is " + compressed.ToString());
31            }
32
33            object nullCheckMaxComponentLength = m_testContext.DataRow["MaximumComponentLength"];
34            if (nullCheckMaxComponentLength.GetType() == typeof(DBNull))
35            {
36                Log.Comment("MaxComponentLength is NULL");
37            }
38            else
39            {
40                UInt32 maxComponentLength = (UInt32)nullCheckMaxComponentLength;
41                Log.Comment("MaxComponentLength is " + maxComponentLength.ToString());
42            }
43
44            object nullCheckAvailability = m_testContext.DataRow["Availability"];
45            if (nullCheckAvailability.GetType() == typeof(DBNull))
46            {
47                Log.Comment("Availability is NULL");
48            }
49            else
50            {
51                UInt32 availability = (UInt32)nullCheckAvailability;
52                Log.Comment("Availability is " + availability.ToString());
53            }
54        }
55        ...
56        public TestContext TestContext
57        {
58            get { return m_testContext; }
59            set { m_testContext = value; }
60        }
61
62        private TestContext m_testContext;
63    }
64}
```

たとえば、上記のテストでは、「圧縮」、"MaximumComponentLength"および"Availability"ことができますを null にするいくつかのシナリオで (クエリでは、フロッピー ディスク ドライブなどのリムーバブル ドライブを返す) 場合。 このような場合、テストが適切に動作するかどうかを確認するには。 このため、オブジェクトとしてプロパティ値を取得および"DBNull"型のかどうかは確認してください。 場合は、返されるプロパティの値が null になります。 Null と有効なため返される値はありませんでしたがない場合 - ので、適切な型にキャストしてのテストに使用します。

ネイティブの取得 Api も使用も同様です - 返されるプロパティの値は NULL にする可能性があります。 これは、(値が null なので、取得することはできませんがある可能性があります) ために、検証の呼び出しを使用せず、値を TestData が正常に取得したかどうかを確認する必要があることを意味します。 たとえば、WMI クエリに依存するテスト メソッドがあります。

```cpp
1        // Test on only local (drive type = 3) or removable (drive type = 2) harddrive
2        BEGIN_TEST_METHOD(LocalOrRemovableHardDriveTest)
3            TEST_METHOD_PROPERTY(L"DataSource", L"WMI:SELECT DeviceId, DriveType, Availability,
                  MaximumComponentLength FROM Win32_LogicalDisk WHERE DriveType=2 OR DriveType=3")
4        END_TEST_METHOD()
```

"可用性と"MaximumComponentLength"が NULL 値として返さ があります。 そのためにこのような対応するテストを記述します。

```cpp
1     void WmiExample::LocalOrRemovableHardDriveTest()
2     {
3         String deviceId;
4         VERIFY_SUCCEEDED(TestData::TryGetValue(L"DeviceId", deviceId));
5         int driveType;
6         VERIFY_SUCCEEDED(TestData::TryGetValue(L"DriveType", driveType));
7
8         unsigned int maxComponentLength;
9         if (SUCCEEDED(TestData::TryGetValue(L"MaximumComponentLength", maxComponentLength)))
10        {
11            Log::Comment(String().Format(L"MaximumComponentLength: %d", maxComponentLength));
12        }
13
14        unsigned int availability;
15        if (SUCCEEDED(TestData::TryGetValue(L"Availability", availability)))
16        {
17            Log::Comment(String().Format(L"Availability: %d", availability));
18        }
19
20        Log::Comment(L"DeviceId: " + deviceId);
21        Log::Comment(String().Format(L"DriveType: %d", driveType));
22    }
```

 

 





