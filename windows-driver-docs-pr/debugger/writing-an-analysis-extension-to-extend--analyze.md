---
title: 分析を拡張するための分析拡張プラグインの作成
description: 分析拡張機能プラグインを記述することで、[デバッガーの分析] コマンドの機能を拡張できます。
ms.assetid: 7648F789-85D5-4247-90DD-2EAA43543483
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab72c46243c129717de6413726abc4462a6bdd3c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834169"
---
# <a name="writing-an-analysis-extension-plugin-to-extend-analyze"></a>Analysis Extension プラグインを記述して拡張する! analyze


Analysis extension プラグインを記述することで、 [ **! analyze**](-analyze.md)デバッガーコマンドの機能を拡張できます。 分析拡張機能プラグインを提供することにより、独自のコンポーネントまたはアプリケーションに固有の方法で、バグチェックまたは例外の分析に参加できます。

分析拡張機能プラグインを記述するときは、プラグインを呼び出す状況を記述したメタデータファイルも記述します。 [ **! Analyze**](-analyze.md)を実行すると、適切な分析拡張機能プラグインが検索、読み込み、および実行されます。

Analysis extension プラグインを作成し、 [ **! analyze**](-analyze.md)で使用できるようにするには、次の手順に従います。

-   [ **\_EFN\_Analyze**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nc-extsfns-ext_analysis_plugin)関数をエクスポートする DLL を作成します。
-   DLL と同じ名前で、拡張子が alz のメタデータファイルを作成します。 たとえば、DLL の名前が MyAnalyzer .dll の場合、メタデータファイルは MyAnalyzer. alz という名前にする必要があります。 メタデータファイルの作成方法の詳細については、「[分析拡張機能のメタデータファイル](metadata-files-for-analysis-extensions.md)」を参照してください。 メタデータファイルを DLL と同じディレクトリに配置します。
-   デバッガーで、 [**extpath**](-extpath--set-extension-path-.md)コマンドを使用して、拡張ファイルパスにディレクトリを追加します。 たとえば、DLL とメタデータファイルが c:\\MyAnalyzer という名前のフォルダーにある場合は、「 **extpath + c:\\MyAnalyzer**」というコマンドを入力します。

[ **! Analyze**](-analyze.md)コマンドがデバッガーで実行されると、分析エンジンは拡張子が alz のメタデータファイルの拡張ファイルパスを検索します。 分析エンジンは、メタデータファイルを読み取って、どの分析拡張プラグインを読み込む必要があるかを判断します。 たとえば、バグチェックの 0xA IRQL に応答して分析エンジンが実行されて\_いて、それよりも少ない\_または\_同等ではない\_、次のエントリを含む MyAnalyzer という名前のメタデータファイルが読み込まれるとします。

```text
PluginId       MyPlugin
DebuggeeClass  Kernel
BugCheckCode   0xA
BugCheckCode   0xE2
```

エントリ `BugCheckCode  0x0A` は、このプラグインがバグチェック0xA の分析に参加する必要があることを指定します。そのため、分析エンジンは、MyAnalyzer .dll (MyAnalyzer と同じディレクトリに存在する必要があります) を読み込み、 [ **\_EFN\_Analyze**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nc-extsfns-ext_analysis_plugin)関数を呼び出します。

**  メタ**データファイルの最後の行は、改行文字で終わる必要があります。

 

## <a name="span-idskeleton_examplespanspan-idskeleton-examplespanspan-idskeleton_examplespanskeleton-example"></a><span id="Skeleton_Example"></span><span id="skeleton-example"></span><span id="SKELETON_EXAMPLE"></span>スケルトンの例


出発点として使用できるスケルトンの例を次に示します。

1.  ここに示されている[ **\_EFN\_Analyze**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nc-extsfns-ext_analysis_plugin)関数をエクスポートする、myanalyzer という名前の dll を作成します。

    ```cpp
    #include <windows.h>
    #define KDEXT_64BIT
    #include <wdbgexts.h>
    #include <dbgeng.h>
    #include <extsfns.h>

    extern "C" __declspec(dllexport) HRESULT _EFN_Analyze(_In_ PDEBUG_CLIENT4 Client, 
       _In_ FA_EXTENSION_PLUGIN_PHASE CallPhase, _In_ PDEBUG_FAILURE_ANALYSIS2 pAnalysis)
    { 
       HRESULT hr = E_FAIL;

       PDEBUG_CONTROL pControl = NULL;
       hr = Client->QueryInterface(__uuidof(IDebugControl), (void**)&pControl);

       if(S_OK == hr && NULL != pControl)
       {
          IDebugFAEntryTags* pTags = NULL;
          pAnalysis->GetDebugFATagControl(&pTags);

          if(NULL != pTags)
          {
             if(FA_PLUGIN_INITILIZATION == CallPhase)
             { 
                pControl->Output(DEBUG_OUTPUT_NORMAL, "My analyzer: initialization\n");  
             }
             else if(FA_PLUGIN_STACK_ANALYSIS == CallPhase)
             {
                pControl->Output(DEBUG_OUTPUT_NORMAL, "My analyzer: stack analysis\n"); 
             }
             else if(FA_PLUGIN_PRE_BUCKETING == CallPhase)
             {
                pControl->Output(DEBUG_OUTPUT_NORMAL, "My analyzer: prebucketing\n");
             }
             else if(FA_PLUGIN_POST_BUCKETING == CallPhase)
             {
                pControl->Output(DEBUG_OUTPUT_NORMAL, "My analyzer: post bucketing\n");    
                FA_ENTRY_TYPE entryType = pTags->GetType(DEBUG_FLR_BUGCHECK_CODE);       
                pControl->Output(DEBUG_OUTPUT_NORMAL, "The data type for the DEBUG_FLR_BUGCHECK_CODE tag is 0x%x.\n\n", entryType);
             }
          }

          pControl->Release();
       }
       return hr;
    }
    ```

2.  次のエントリを持つ MyAnalyzer という名前のメタデータファイルを作成します。

    ```text
    PluginId      MyPlugin
    DebuggeeClass Kernel
    BugCheckCode  0xE2
    ```

    **  メタ**データファイルの最後の行は、改行文字で終わる必要があります。

     

3.  ホストとターゲットコンピューターの間でカーネルモードのデバッグセッションを確立します。

4.  ホストコンピューターで、myanalyzer .dll と MyAnalyzer をフォルダー c:\\MyAnalyzer に配置します。

5.  ホストコンピューターのデバッガーで、次のコマンドを入力します。

    **. extpath + c:\\MyAnalyzer**

    **. クラッシュ**

6.  Crash コマンドを実行すると、ターゲットコンピューター上で\_クラッシュ\_手動で生成され[**ます。** ](-crash--force-system-crash-.md)これにより、ホストコンピューター上のデバッガーが中断されます。 (ホストコンピューター上のデバッガーで実行されている) バグチェック分析エンジンは、MyAnalyzer. alz を読み取り、MyAnalyzer .dll がバグチェック0xE2 の分析に参加できることを確認します。 このため、分析エンジンは、MyAnalyzer .dll を読み込み、 [ **\_EFN\_Analyze**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nc-extsfns-ext_analysis_plugin)関数を呼び出します。

    デバッガーで、次のような出力が表示されていることを確認します。

    ```dbgcmd
    *                        Bugcheck Analysis                                    *
    *                                                                             *
    *******************************************************************************

    Use !analyze -v to get detailed debugging information.

    BugCheck E2, {0, 0, 0, 0}

    My analyzer: initialization
    My analyzer: stack analysis
    My analyzer: prebucketing
    My analyzer: post bucketing
    The data type for the DEBUG_FLR_BUGCHECK_CODE tag is 0x1.
    ```

上記のデバッガー出力は、分析エンジンが[ **\_EFN\_Analyze**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nc-extsfns-ext_analysis_plugin)関数を4回呼び出したことを示しています。これは、分析の各フェーズで1回実行されます。 分析エンジンは、 **\_EFN\_Analyze**関数の2つのインターフェイスポインターを渡します。 *クライアント*は[**IDebugClient4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugclient4)インターフェイスで、 *pAnalysis*は[**IDebugFailureAnalysis2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)インターフェイスです。 前のスケルトンの例のコードは、さらに2つのインターフェイスポインターを取得する方法を示しています。 `Client->QueryInterface` は[**IDebugControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugcontrol)インターフェイスを取得し、`pAnalysis->GetDebugFATagControl` **IDebugFAEntryTags**インターフェイスを取得します。

## <a name="span-idfailure-analysis-entries-tags-and-data-typesspanspan-idfailure_analysis_entries_tags_and_data_typesspanfailure-analysis-entries-tags-and-data-types"></a><span id="failure-analysis-entries-tags-and-data-types"></span><span id="FAILURE_ANALYSIS_ENTRIES_TAGS_AND_DATA_TYPES"></span>失敗の分析のエントリ、タグ、およびデータ型


分析エンジンは、特定のコードエラーに関連するデータを整理するための[**Debugfailureanalysis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)オブジェクトを作成します。 **Debugfailureanalysis**オブジェクトには、[エラー分析エントリ](failure-analysis-entries.md)(fa エントリ) のコレクションが含まれており、それぞれが**fa\_エントリ**構造によって表されます。 Analysis extension プラグインは、 **IDebugFailureAnalysis2**インターフェイスを使用して、この FA エントリのコレクションにアクセスします。 各 FA エントリには、エントリに含まれる情報の種類を識別するタグがあります。 たとえば、FA エントリには、**デバッグ\_FLR\_バグチェック\_コード**が含まれている可能性があります。これにより、エントリにバグチェックコードが含まれていることがわかります。 タグは、 **DEBUG\_FLR\_PARAM\_TYPE**列挙体の値です (extsfns で定義されています)。これは、 **FA\_タグ**の列挙とも呼ばれます。

```cpp
typedef enum _DEBUG_FLR_PARAM_TYPE {
    ...
    DEBUG_FLR_BUGCHECK_CODE,
    ...
    DEBUG_FLR_BUILD_VERSION_STRING,
    ...
} DEBUG_FLR_PARAM_TYPE;

typedef DEBUG_FLR_PARAM_TYPE FA_TAG;
```

ほとんどの[FA エントリ](failure-analysis-entries.md)には、関連付けられたデータブロックがあります。 **FA\_エントリ**構造の**DataSize**メンバーは、データブロックのサイズを保持します。 一部の FA エントリには、関連付けられたデータブロックがありません。すべての情報は、タグによって伝達されます。 このような場合、 **DataSize**メンバーの値は0です。

```cpp
typedef struct _FA_ENTRY
{
    FA_TAG Tag;
    USHORT FullSize;
    USHORT DataSize;
} FA_ENTRY, *PFA_ENTRY;
```

各タグには、名前、説明、データ型などの一連のプロパティがあります。 [**Debugfailureanalysis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)オブジェクトは、タグプロパティのコレクションを含む[DebugFailureAnalysisTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfaentrytags)オブジェクトに関連付けられています。 次の図は、この関連付けを示しています。

![分析エンジン、debugfailureanalysis オブジェクト、および debugfailureanalysistags オブジェクトを示す図](images/debugfa01.png)

[**Debugfailureanalysis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)オブジェクトには、特定の分析セッションに属する[FA エントリ](failure-analysis-entries.md)のコレクションがあります。 関連付けられた[DebugFailureAnalysisTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfaentrytags)オブジェクトには、同じ分析セッションで使用されるタグのみを含むタグプロパティのコレクションがあります。 上の図に示すように、分析エンジンには、分析セッションで一般に使用可能な多数のタグに関する制限された情報を保持するグローバルタグテーブルがあります。

通常、分析セッションで使用されるタグのほとんどは標準タグです。つまり、タグは、 [**FA\_タグ**](https://docs.microsoft.com/previous-versions/jj991810(v=vs.85))列挙の値です。 ただし、analysis extension プラグインではカスタムタグを作成できます。 分析拡張機能のプラグインでは、 [**Debugfailureanalysis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)オブジェクトに[FA エントリ](failure-analysis-entries.md)を追加し、エントリのカスタムタグを指定できます。 その場合、カスタムタグのプロパティは、関連付けられている[DebugFailureAnalysisTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfaentrytags)オブジェクトのタグプロパティのコレクションに追加されます。

IDebugFAEntry tags インターフェイスを使用して[DebugFailureAnalysisTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfaentrytags)にアクセスできます。 IDebugFAEntry インターフェイスへのポインターを取得するには、 [**IDebugFailureAnalysis2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)インターフェイスの[**Getdebugfat agcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nf-extsfns-idebugfailureanalysis2-getdebugfatagcontrol)メソッドを呼び出します。

各タグには、データ型のプロパティがあります。このプロパティを調べて、エラー分析エントリのデータのデータ型を確認できます。 データ型は、 **FA\_ENTRY\_type 列挙型**の値によって表されます。

次のコード行は、**デバッグ\_FLR\_BUILD\_VERSION\_STRING**タグのデータ型を取得します。 この場合、データ型は、 **ANSI\_文字列\_の FA\_エントリ\_デバッグ**です。 コードでは、`pAnalysis` は[**IDebugFailureAnalysis2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)インターフェイスへのポインターです。

```cpp
IDebugFAEntryTags* pTags = pAnalysis->GetDebugFATagControl(&pTags);

if(NULL != pTags)
{
   FA_ENTRY_TYPE entryType = pTags->GetType(DEBUG_FLR_BUILD_VERSION_STRING);
}
```

エラー分析エントリにデータブロックがない場合、関連付けられているタグのデータ型は**デバッグ\_FA\_エントリ\_\_種類はありません**。

[**Debugfailureanalysis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)オブジェクトには、 [FA エントリ](failure-analysis-entries.md)のコレクションがあることを思い出してください。 コレクション内のすべての FA エントリを検査するには、 **NextEntry**メソッドを使用します。 次の例は、FA エントリのコレクション全体を反復処理する方法を示しています。 *PAnalysis*が**IDebugFailureAnalysis2**インターフェイスへのポインターであると仮定します。 **NextEntry**に**NULL**を渡すことによって最初のエントリを取得することに注意してください。

```cpp
PFA_ENTRY entry = pAnalysis->NextEntry(NULL);

while(NULL != entry)
{
   // Do something with the entry

   entry = pAnalysis->NextEntry(entry);
}
```

タグには、名前と説明を含めることができます。 次のコードでは、 *pAnalysis*は[**IDebugFailureAnalysis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)インターフェイスへのポインターであり、 *pcontrol*は[**IDebugControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugcontrol)インターフェイスへのポインターであり、`pTags` は[IDebugFAEntryTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfaentrytags)インターフェイスへのポインターです。 このコードは、 **GetProperties**メソッドを使用して、 [FA エントリ](failure-analysis-entries.md)に関連付けられたタグの名前と説明を取得する方法を示しています。

```cpp
#define MAX_NAME_LENGTH 64
#define MAX_DESCRIPTION_LENGTH 512

CHAR name[MAX_NAME_LENGTH] = {0};
ULONG nameSize = MAX_NAME_LENGTH;
CHAR desc[MAX_DESCRIPTION_LENGTH] = {0};
ULONG descSize = MAX_DESCRIPTION_LENGTH;
                  
PFA_ENTRY pEntry = pAnalysis->NextEntry(NULL); 
pTags->GetProperties(pEntry->Tag, name, &nameSize, desc, &descSize, NULL);
pControl->Output(DEBUG_OUTPUT_NORMAL, "The name is %s\n", name);
pControl->Output(DEBUG_OUTPUT_NORMAL, "The description is %s\n", desc);
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[カスタム分析デバッガー拡張機能の作成](writing-custom-analysis-debugger-extensions.md)

[ **\_EFN\_分析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nc-extsfns-ext_analysis_plugin)

[分析拡張プラグインのメタデータファイル](metadata-files-for-analysis-extensions.md)

[**IDebugFailureAnalysis2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)

[IDebugFAEntryTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfaentrytags)

 

 






