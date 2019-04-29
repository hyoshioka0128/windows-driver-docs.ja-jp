---
title: 分析の拡張機能プラグインを拡張に書き込む分析
description: 分析の拡張機能プラグインを記述することで、分析のデバッガー コマンドの機能を拡張できます。
ms.assetid: 7648F789-85D5-4247-90DD-2EAA43543483
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7dd1b8c31c7a80c9f1efdc12cfc69d0b9cb84365
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383741"
---
# <a name="writing-an-analysis-extension-plugin-to-extend-analyze"></a>分析の拡張機能プラグインを拡張する記述! 分析


機能を拡張することができます、 [ **! 分析**](-analyze.md)分析の拡張機能プラグインを記述することでデバッガー コマンド。 分析の拡張機能プラグインを提供するには、によっては、バグ チェックや、独自のコンポーネントまたはアプリケーションに固有の方法での例外の解析に参加できます。

分析の拡張機能プラグインを記述するときに、呼び出されるプラグインの対象となる状況を説明するメタデータ ファイルを記述します。 ときに[ **! 分析**](-analyze.md)実行されると、検索、読み込み、および適切な分析の拡張機能プラグインを実行します。

分析の拡張機能プラグインを記述し、使用できるようにする[ **! 分析**](-analyze.md)、これらの手順に従います。

-   エクスポートする DLL を作成、 [  **\_EFN\_分析**](https://msdn.microsoft.com/library/windows/hardware/jj983432)関数。
-   DLL と .alz の拡張機能と同じ名前を持つメタデータ ファイルを作成します。 たとえば、MyAnalyzer.dll、DLL の名前が場合、メタデータする必要があるという名前のファイル MyAnalyzer.alz します。 メタデータ ファイルを作成する方法については、次を参照してください。[分析拡張機能のメタデータ ファイル](metadata-files-for-analysis-extensions.md)します。 DLL と同じディレクトリにメタデータ ファイルを配置します。
-   デバッガーで使用して、 [ **.extpath** ](-extpath--set-extension-path-.md)拡張ファイルのパスにディレクトリを追加するコマンド。 たとえば、DLL とメタデータ ファイルが c: という名前のフォルダーは\\MyAnalyzer、コマンドを入力して **.extpath + c:\\MyAnalyzer**。

ときに、 [ **! 分析**](-analyze.md)コマンドは、デバッガーで実行、分析エンジンが .alz 拡張子を持つメタデータ ファイルの拡張機能のファイル パスで検索します。 分析エンジンはどの分析拡張機能プラグインを読み込む必要がありますかを決定するメタデータ ファイルを読み取ります。 たとえば、0 xa のバグ チェックへの応答で分析エンジンが実行されている IRQL\_いない\_少ない\_または\_等しく、また、次のエントリを含む MyAnalyzer.alz をという名前のメタデータ ファイルを読み取ります。

```text
PluginId       MyPlugin
DebuggeeClass  Kernel
BugCheckCode   0xA
BugCheckCode   0xE2
```

エントリ`BugCheckCode  0x0A`このプラグインは、分析エンジンを読み込みます (MyAnalyzer.alz と同じディレクトリである必要があります) を MyAnalyzer.dll と呼び出しのためのバグ チェック 0 xa、分析に参加する必要があるを指定しますその[  **\_。EFN\_分析**](https://msdn.microsoft.com/library/windows/hardware/jj983432)関数。

**注**  メタデータ ファイルの最後の行は改行文字で終わる必要があります。

 

## <a name="span-idskeletonexamplespanspan-idskeleton-examplespanspan-idskeletonexamplespanskeleton-example"></a><span id="Skeleton_Example"></span><span id="skeleton-example"></span><span id="SKELETON_EXAMPLE"></span>スケルトンの例


開始点として使用できるスケルトンの例を次に示します。

1.  エクスポートする MyAnalyzer.dll という名前の DLL をビルド、 [  **\_EFN\_分析**](https://msdn.microsoft.com/library/windows/hardware/jj983432)関数を次に示します。

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

2.  次のエントリを持つ MyAnalyzer.alz をという名前のメタデータ ファイルを作成します。

    ```text
    PluginId      MyPlugin
    DebuggeeClass Kernel
    BugCheckCode  0xE2
    ```

    **注**  メタデータ ファイルの最後の行は改行文字で終わる必要があります。

     

3.  ホストおよびターゲット コンピューターの間でカーネル モードのデバッグ セッションを確立します。

4.  ホスト コンピューターでは、フォルダー c: MyAnalyzer.dll と MyAnalyzer.alz に配置\\MyAnalyzer します。

5.  ホスト コンピューターでは、デバッガーでこれらのコマンドを入力します。

    **.extpath + c:\\MyAnalyzer**

    **.crash**

6.  [ **.Crash** ](-crash--force-system-crash-.md) 0 xe2 のバグ チェックを手動で生成コマンド\_INITIATED\_対象のコンピューター、ホスト コンピューター上のデバッガーの中断が原因でクラッシュします。 バグ チェックの分析エンジン (ホスト コンピューターで、デバッガーで実行されている) は、MyAnalyzer.alz を読み取って、MyAnalyzer.dll が 0 xe2 のバグ チェックの分析に参加できることを認識します。 分析エンジンは、MyAnalyzer.dll と呼び出しを読み込むようにその[  **\_EFN\_分析**](https://msdn.microsoft.com/library/windows/hardware/jj983432)関数。

    デバッガーでは、次のような出力が表示されることを確認します。

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

上記のデバッガーの出力は、分析エンジンが呼び出されることを示しています、 [  **\_EFN\_分析**](https://msdn.microsoft.com/library/windows/hardware/jj983432) 4 回の機能: 分析の段階ごとに 1 回です。 分析エンジンに渡す、  **\_EFN\_分析**関数の 2 つのインターフェイス ポインター。 *クライアント*は、 [ **IDebugClient4** ](https://msdn.microsoft.com/library/windows/hardware/ff550494)インターフェイス、および*pAnalysis*は、 [ **IDebugFailureAnalysis2**](https://msdn.microsoft.com/library/windows/hardware/jj983405)インターフェイス。 上記のスケルトン内のコードでは、2 つ以上のインターフェイス ポインターを取得する方法を示します。 `Client->QueryInterface` 取得、 [ **IDebugControl** ](https://msdn.microsoft.com/library/windows/hardware/ff550508)インターフェイス、および`pAnalysis->GetDebugFATagControl`を取得、 **IDebugFAEntryTags**インターフェイス。

## <a name="span-idfailure-analysis-entries-tags-and-data-typesspanspan-idfailureanalysisentriestagsanddatatypesspanfailure-analysis-entries-tags-and-data-types"></a><span id="failure-analysis-entries-tags-and-data-types"></span><span id="FAILURE_ANALYSIS_ENTRIES_TAGS_AND_DATA_TYPES"></span>エラー分析のエントリ、タグ、およびデータ型


分析エンジンを作成、 [ **DebugFailureAnalysis** ](https://msdn.microsoft.com/library/windows/hardware/jj983405)データを整理するオブジェクトが特定のコードの不具合に関係します。 A **DebugFailureAnalysis**オブジェクトのコレクションがある[エラー分析のエントリ](failure-analysis-entries.md)(FA エントリ)、それぞれがによって表される、 **FA\_エントリ**構造体. 分析の拡張機能プラグインを使用して、 **IDebugFailureAnalysis2** FA エントリのこのコレクションへのアクセスを取得するインターフェイス。 FA の各エントリでは、エントリが含まれている情報の種類を識別するタグがあります。 たとえば、FA のエントリは、タグがある**デバッグ\_FLR\_バグチェック\_コード**バグの確認コードには、エントリが含まれているを指定します。 タグの値には、**デバッグ\_FLR\_PARAM\_型**(extsfns.h で定義されている) とも呼ばれる列挙、 **FA\_タグ**列挙体。

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

ほとんど[FA エントリ](failure-analysis-entries.md)関連付けられているデータ ブロックがあります。 **DataSize**のメンバー、 **FA\_エントリ**構造体は、データ ブロックのサイズを保持します。 FA エントリをいくつかは、ブロックに関連付けられているデータがありません。すべての情報を伝達するには、タグを使用しています。 これらの場合、 **DataSize**メンバーが 0 の値を持ちます。

```cpp
typedef struct _FA_ENTRY
{
    FA_TAG Tag;
    USHORT FullSize;
    USHORT DataSize;
} FA_ENTRY, *PFA_ENTRY;
```

各タグが一連のプロパティ: たとえば、名前、説明、およびデータ型。 A [ **DebugFailureAnalysis** ](https://msdn.microsoft.com/library/windows/hardware/jj983405)オブジェクトが関連付けられている、 [DebugFailureAnalysisTags](https://msdn.microsoft.com/library/windows/hardware/jj983404)タグ プロパティのコレクションを含むオブジェクトです。 次の図は、この関連付けを示します。

![分析エンジン、debugfailureanalysis オブジェクト、および debugfailureanalysistags オブジェクトを示す図](images/debugfa01.png)

A [ **DebugFailureAnalysis** ](https://msdn.microsoft.com/library/windows/hardware/jj983405)オブジェクトのコレクションがある[FA エントリ](failure-analysis-entries.md)特定の分析セッションに属しています。 関連付けられている[DebugFailureAnalysisTags](https://msdn.microsoft.com/library/windows/hardware/jj983404)オブジェクトにタグのプロパティのコレクションであり、その同じ分析セッションで使用されるタグのみが含まれています。 前の図に示す、分析エンジンは、大規模な分析セッションで使用するために一般的に使用できるタグを一連の限定された情報を格納しているグローバル タグ テーブル。

通常、分析セッションで使用されるタグのほとんどでは、標準のタグタグは内の値、つまり、 [ **FA\_タグ**](https://msdn.microsoft.com/library/windows/hardware/jj991810)列挙体。 ただし、プラグイン分析拡張機能は、カスタム タグを作成することができます。 プラグイン分析拡張機能を追加、 [FA エントリ](failure-analysis-entries.md)を[ **DebugFailureAnalysis** ](https://msdn.microsoft.com/library/windows/hardware/jj983405)オブジェクトし、エントリのカスタム タグを指定します。 関連付けられているタグのプロパティのコレクションにカスタム タグのプロパティを追加する場合、 [DebugFailureAnalysisTags](https://msdn.microsoft.com/library/windows/hardware/jj983404)オブジェクト。

アクセスできる、 [DebugFailureAnalysisTags](https://msdn.microsoft.com/library/windows/hardware/jj983404) IDebugFAEntry をインターフェイスにタグを付けます。 IDebugFAEntry インターフェイスへのポインターを取得する、 [ **GetDebugFATagControl** ](https://msdn.microsoft.com/library/windows/hardware/jj983414)のメソッド、 [ **IDebugFailureAnalysis2** ](https://msdn.microsoft.com/library/windows/hardware/jj983405)インターフェイスです。

各タグには、データ エラーの分析のエントリ内のデータのデータ型を決定する際に調べることができますプロパティの型があります。 内の値によって表されるデータ型、 **FA\_エントリ\_型**列挙体。

次のコード行のデータ型を取得する、**デバッグ\_FLR\_ビルド\_バージョン\_文字列**タグ。 データ型は、この場合、**デバッグ\_FA\_エントリ\_ANSI\_文字列**します。 コードでは、`pAnalysis`へのポインター、 [ **IDebugFailureAnalysis2** ](https://msdn.microsoft.com/library/windows/hardware/jj983405)インターフェイス。

```cpp
IDebugFAEntryTags* pTags = pAnalysis->GetDebugFATagControl(&pTags);

if(NULL != pTags)
{
   FA_ENTRY_TYPE entryType = pTags->GetType(DEBUG_FLR_BUILD_VERSION_STRING);
}
```

関連付けられているタグのデータ型は、エラーの分析のエントリには、データ ブロックがなければ、**デバッグ\_FA\_エントリ\_ありません\_型**します。

いることを思い出してください、 [ **DebugFailureAnalysis** ](https://msdn.microsoft.com/library/windows/hardware/jj983405)オブジェクトのコレクションがある[FA エントリ](failure-analysis-entries.md)します。 コレクション内のすべての FA エントリを検査するを使用して、 **NextEntry**メソッド。 次の例では、FA エントリのコレクション全体を反復処理する方法を示します。 ある*pAnalysis*へのポインター、 **IDebugFailureAnalysis2**インターフェイス。 最初のエントリを渡すことによって取得に注目してください。 **NULL**に**NextEntry**します。

```cpp
PFA_ENTRY entry = pAnalysis->NextEntry(NULL);

while(NULL != entry)
{
   // Do something with the entry

   entry = pAnalysis->NextEntry(entry);
}
```

名前と説明、タグを持つことができます。 次のコードで*pAnalysis*へのポインター、 [ **IDebugFailureAnalysis** ](https://msdn.microsoft.com/library/windows/hardware/jj983405)インターフェイス、 *pControl* へのポインターです[**IDebugControl** ](https://msdn.microsoft.com/library/windows/hardware/ff550508)インターフェイス、および`pTags`へのポインター、 [IDebugFAEntryTags](https://msdn.microsoft.com/library/windows/hardware/jj983404)インターフェイス。 コードを使用する方法を示します、 **GetProperties**に関連付けられているタグの説明と名前を取得するメソッド、 [FA エントリ](failure-analysis-entries.md)します。

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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[カスタム分析デバッガー拡張機能の作成](writing-custom-analysis-debugger-extensions.md)

[**\_EFN\_分析**](https://msdn.microsoft.com/library/windows/hardware/jj983432)

[メタデータ ファイルを分析拡張機能プラグイン](metadata-files-for-analysis-extensions.md)

[**IDebugFailureAnalysis2**](https://msdn.microsoft.com/library/windows/hardware/jj983405)

[IDebugFAEntryTags](https://msdn.microsoft.com/library/windows/hardware/jj983404)

 

 






