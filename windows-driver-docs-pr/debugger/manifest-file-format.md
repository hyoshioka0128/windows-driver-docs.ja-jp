---
title: マニフェスト ファイルの形式
description: マニフェスト ファイルの形式
ms.assetid: 1b0dc305-878c-4eb2-9e92-f7f7017ae4eb
keywords:
- LogViewer、マニフェスト、ファイルの形式
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b289e0d526d5906528b4112ddb56836ae1eca60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532024"
---
# <a name="manifest-file-format"></a>マニフェスト ファイルの形式


## <span id="ddk_manifest_file_format_dtoolq"></span><span id="DDK_MANIFEST_FILE_FORMAT_DTOOLQ"></span>


マニフェスト ファイルのファイル形式は、可能な C++ および IDL から多くの部分で利用します。 その結果、通常の C++ SDK ヘッダー ファイルを実行し、マニフェスト ファイルを変更する方が簡単です。 パーサーは、整理し、ファイルを文書化する C および C++ スタイルのコメントを完全にサポートします。

マニフェスト ファイルを追加または既存のファイルを変更する場合は、これを行う最善の方法が、実験が必要です。 発行するとき、 **! logexts.logi**または **! logexts.loge**ロガーはマニフェスト ファイルを解析しようとします。 デバッガーで、コマンド。 問題が発生すると、誤りの可能性を示すエラー メッセージが生成されます。

次の基本的な要素のマニフェスト ファイルから成る: モジュールのラベル、カテゴリのラベル、関数の宣言、COM インターフェイスの定義、および種類の定義。 同様に、その他の種類の要素が存在するが、これらは、最も重要です。

### <a name="span-idmodulelabelsspanspan-idmodulelabelsspanmodule-labels"></a><span id="module_labels"></span><span id="MODULE_LABELS"></span>モジュールのラベル

モジュールのラベルは、DLL のエクスポート後に宣言されている関数を宣言します。 たとえば、マニフェスト ファイルが Comctl32.dll から関数のグループのログ記録の場合、関数プロトタイプを宣言する前に次のモジュールのラベルを含めます。

```cpp
module COMCTL32.DLL:
```

モジュールのラベルは、マニフェスト ファイルで関数宣言の前に表示する必要があります。 マニフェスト ファイルは、任意の数のモジュールのラベルを含めることができます。

### <a name="span-idcategorylabelsspanspan-idcategorylabelsspancategory-labels"></a><span id="category_labels"></span><span id="CATEGORY_LABELS"></span>カテゴリ ラベル

モジュールのラベルと同様に、カテゴリのラベルは「カテゴリ」に属しているすべての後続の関数や COM インターフェイスを識別します。 たとえば、Comctl32.dll のマニフェスト ファイルを作成する場合は、カテゴリのラベルとして、次を使用できます。

```cpp
category CommonControls:
```

マニフェスト ファイルは、任意の数のカテゴリのラベルを含めることができます。

### <a name="span-idfunctiondeclarationsspanspan-idfunctiondeclarationsspanfunction-declarations"></a><span id="function_declarations"></span><span id="FUNCTION_DECLARATIONS"></span>関数の宣言

関数宣言は、実際に何かをログするロガーを求めるものです。 C/C++ ヘッダー ファイルで見つかった関数プロトタイプとほぼ同じになります。 形式は、次の例で最適に示します、いくつか注目すべき追加機能があります。

```cpp
HANDLE [gle] FindFirstFileA(
       LPCSTR lpFileName,
       [out] LPWIN32_FIND_DATAA lpFindFileData);
```

関数は、 **FindFirstFileA**は 2 つのパラメーターを受け取ります。 1 つは、 *lpFileName*これは、ファイルまたはファイルを検索する場所を定義する (通常はワイルドカード文字) で完全なパスです。 2 つ目は、WIN32 へのポインター\_検索\_DATAA 構造検索結果を格納するために使用されます。 今後の呼び出しに対して、返されたハンドルが使用される**FindNextFileA**します。 場合**FindFirstFileA**返します無効な\_処理\_値、関数呼び出しに失敗し、エラー コードを呼び出すことによって調達でき、 **GetLastError**関数。

ハンドル型は、次のように宣言されます。

```cpp
value DWORD HANDLE
{
#define NULL                       0 [fail]
#define INVALID_HANDLE_VALUE      -1 [fail]
};
```

この関数によって返される値が 0 または-1 (0 xffffffff) の場合は、ロガーが前提としています、関数が失敗したこと、このような値があるため、\[失敗\]値宣言の修飾子。 (このセクションで後で値型のセクションを参照)。あるため、 \[gle\]関数名の直前の修飾子、ロガーの認識がこの関数を使用している**GetLastError**をエラー コードをキャプチャし、ログ ファイルにログに記録するために、エラー コードを返します。

\[アウト\]修飾子を*lpFindFileData*パラメーター データ構造体、関数によってが入力されており、関数が返されるときにログに記録する必要がありますを Logger に通知します。

### <a name="span-idcominterfacedefinitionsspanspan-idcominterfacedefinitionsspancom-interface-definitions"></a><span id="com_interface_definitions"></span><span id="COM_INTERFACE_DEFINITIONS"></span>COM インターフェイスの定義

COM インターフェイスは、基本的に、COM オブジェクトのクライアントで呼び出すことができる関数のベクトルです。 マニフェストの形式でインターフェイスを定義する COM で使用されるインターフェイス定義言語 (IDL) から利用大きくします。

次の例を検討してください。

```cpp
interface IDispatch : IUnknown
{
    HRESULT GetTypeInfoCount( UINT pctinfo  );
 
    HRESULT GetTypeInfo(
        UINT iTInfo,
        LCID lcid,
        LPVOID ppTInfo );
 
    HRESULT GetIDsOfNames(
        REFIID riid,
        LPOLECHAR* rgszNames,
        UINT cNames,
        LCID lcid,
        [out] DISPID* rgDispId );
 
    HRESULT Invoke( 
        DISPID  dispIdMember,      
        REFIID  riid,              
        LCID  lcid,                
        WORD  wFlags,              
        DISPPARAMS*  pDispParams,  
        VARIANT*  pVarResult,  
        EXCEPINFO*  pExcepInfo,  
        UINT*  puArgErr );
};
```

これと呼ばれるインターフェイスを宣言します。 **IDispatch**から派生する**IUnknown**します。 インターフェイスの中かっこ内の特定の順序で宣言される 4 つのメンバー関数が含まれています。 ロガーはインターセプトし、独自のインターフェイスの vtable (実行時に使用される関数ポインターの実際のバイナリ ベクトル) の関数ポインターを置き換えることで、これらのメンバー関数のログします。 COM を参照してください。\_インターフェイス\_PTR タイプ セクションが配布されたようにロガーがインターフェイスをキャプチャする方法の詳細については、このセクションで後述します。

### <a name="span-idtypedefinitionsspanspan-idtypedefinitionsspantype-definitions"></a><span id="type_definitions"></span><span id="TYPE_DEFINITIONS"></span>型の定義

データ型の定義は、マニフェスト ファイルの開発の最も重要な (および最も面倒な) の一部です。 マニフェスト、言語に渡される、関数から返される数値の人間が判読できるラベルを定義することができます。

たとえば、Winerror.h は"WinError"と呼ばれる型を定義します。 ほとんどの Microsoft Win32 関数とその対応する人間が判読できるラベルによって返されるエラー値のリストであります。 これにより、Logger と LogViewer uninformative エラー コードを意味のあるテキストに置き換えます。

ロガーを許可するビット マスク内の個々 のビット ラベル付けすることもでき、DWORD を中断する LogViewer ビット マスクをそのコンポーネントにします。

マニフェストでサポートされている 13 の基本的な種類があります。 これらは、次の表に表示されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">種類</th>
<th align="left">長さ</th>
<th align="left">表示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ポインター</p></td>
<td align="left"><p>4 バイト</p></td>
<td align="left"><p>0x001AF320</p></td>
</tr>
<tr class="even">
<td align="left"><p>VOID</p></td>
<td align="left"><p>0 バイト</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>BYTE</p></td>
<td align="left"><p>1 バイト</p></td>
<td align="left"><p>0x32</p></td>
</tr>
<tr class="even">
<td align="left"><p>WORD</p></td>
<td align="left"><p>2 バイト</p></td>
<td align="left"><p>0x0A23</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DWORD</p></td>
<td align="left"><p>4 バイト</p></td>
<td align="left"><p>-234323</p></td>
</tr>
<tr class="even">
<td align="left"><p>BOOL</p></td>
<td align="left"><p>1 バイト</p></td>
<td align="left"><p><strong>TRUE</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>LPSTR</p></td>
<td align="left"><p>バイトの長さと文字の任意の数</p></td>
<td align="left"><p>&quot;クイック brown fox&quot;</p></td>
</tr>
<tr class="even">
<td align="left"><p>LPWSTR</p></td>
<td align="left"><p>バイトの長さと Unicode 文字の任意の数</p></td>
<td align="left"><p>&quot;亜ジャンプ&quot;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GUID</p></td>
<td align="left"><p>16 バイト</p></td>
<td align="left"><p>{0CF774D0-F077-11D1-B1BC-00C04F86C324}</p></td>
</tr>
<tr class="even">
<td align="left"><p>COM_INTERFACE_PTR</p></td>
<td align="left"><p>4 バイト</p></td>
<td align="left"><p>0x0203404A</p></td>
</tr>
<tr class="odd">
<td align="left"><p>value</p></td>
<td align="left"><p>基本データ型に依存</p></td>
<td align="left"><p>ERROR_TOO_MANY_OPEN_FILES</p></td>
</tr>
<tr class="even">
<td align="left"><p>マスク</p></td>
<td align="left"><p>基本データ型に依存</p></td>
<td align="left"><p>WS_MAXIMIZED | WS_ALWAYSONTOP</p></td>
</tr>
<tr class="odd">
<td align="left"><p>構造体</p></td>
<td align="left"><p>カプセル化された型のサイズに依存</p></td>
<td align="left"><p></p>
+ lpRect nLeft 34 nRight 54 nTop 100 nBottom 300</td>
</tr>
</tbody>
</table>

 

C と C++ の typedef のようにマニフェスト ファイルの作業では、定義を入力します。 たとえば、次のステートメントでは、長整数型へのポインターとして PLONG を定義します。

```cpp
typedef LONG *PLONG;
```

Main.h で、最も基本的な typedef は既に宣言されています。 コンポーネントに固有の typedef を追加する必要がだけする必要があります。 構造体の定義がある C/C++ 構造体の型と同じ形式です。

次の 4 つの特殊な種類があります: 値、マスク、GUID、および COM\_インターフェイス\_PTR。

<span id="Value_Types"></span><span id="value_types"></span><span id="VALUE_TYPES"></span>値型  
値は、人間が判読できるラベルに分類が基本型です。 ほとんどの関数のドキュメントのみを参照する、 **\#定義**関数で使用される特定の定数の値。 たとえば、プログラマのほとんどが、実際の値がによって返されるすべてのコードに対しては認識していない**GetLastError**LogViewer で暗号のような数値を表示する役に立たないようにします。 マニフェストの値は、次の例に示すように値の宣言を許可することでこれを克服します。

```cpp
value LONG ChangeNotifyFlags
{
#define SHCNF_IDLIST      0x0000        // LPITEMIDLIST
#define SHCNF_PATHA       0x0001        // path name
#define SHCNF_PRINTERA    0x0002        // printer friendly name
#define SHCNF_DWORD       0x0003        // DWORD
#define SHCNF_PATHW       0x0005        // path name
#define SHCNF_PRINTERW    0x0006        // printer friendly name
};
```

これは、時間の長いから派生した"ChangeNotifyFlags"と呼ばれる新しい型を宣言します。 これは、関数パラメーターとして使用して、生の数値の代わりに、人間が判読できるエイリアスが表示されます。

<span id="Mask_Types"></span><span id="mask_types"></span><span id="MASK_TYPES"></span>マスクの種類  
値の型と同様に、マスクの種類は、基本的な型 (通常は DWORD) の意味を持つビットのそれぞれの人間が判読できるラベルに分類されます。 次の例を実行します。

```cpp
mask DWORD DirectDrawOptSurfaceDescCapsFlags
{
#define DDOSDCAPS_OPTCOMPRESSED                 0x00000001
#define DDOSDCAPS_OPTREORDERED                  0x00000002
#define DDOSDCAPS_MONOLITHICMIPMAP              0x00000004
};
```

これを関数のパラメーターとして使用する場合に LogViewer 内のユーザーの内訳が個別の値を持つ DWORD から派生した新しい型を宣言します。 そのため、値が 0x00000005 の場合は、LogViewer が表示されます。

```cpp
DDOSDCAPS_OPTCOMPRESSED | DDOSDCAPS_MONOLITHICMIPMAP
```

<span id="GUID_Types"></span><span id="guid_types"></span><span id="GUID_TYPES"></span>GUID 型  
Guid は、COM で広く使用されている 16 バイトのグローバル一意識別子 これらは、2 つの方法で宣言されます。

```cpp
struct __declspec(uuid("00020400-0000-0000-C000-000000000046")) IDispatch;
```

または

```cpp
class __declspec(uuid("11219420-1768-11D1-95BE-00609797EA4F")) ShellLinkObject;
```

最初のメソッドは、インターフェイス id (IID) の宣言に使用されます。 LogViewer、によって表示されるときに"IID\_"表示名の先頭に追加されます。 2 番目のメソッドは、クラス id (CLSID) を宣言に使用されます。 LogViewer を追加します"CLSID\_"表示名の先頭にします。

GUID 型が関数のパラメーターの場合は、LogViewer はに対して宣言されているすべての Iid および Clsid 値を比較します。 一致が見つかった場合は、IID フレンドリ名が表示されます。 それ以外の場合は、標準の GUID の表記法で 32 桁 16 進数の値が表示されます。

<span id="COM_INTERFACE_PTR_Types"></span><span id="com_interface_ptr_types"></span><span id="COM_INTERFACE_PTR_TYPES"></span>COM\_インターフェイス\_PTR の種類  
COM\_インターフェイス\_PTR 型は COM インターフェイス ポインターの基本型です。 COM から派生した新しい型を定義する実際に COM インターフェイスを宣言するときに\_インターフェイス\_PTR。 そのため、このような型へのポインターは関数のパラメーターを指定できます。 場合、COM\_インターフェイス\_PTR の基本的な型が関数に OUT パラメーターとして宣言されており、個別のパラメーターがある、 \[iid\]ラベル、ロガーは渡された IID に対して宣言されたすべての Guid を比較します。 一致がある COM インターフェイスの IID と同じ名前を持つが宣言された場合は、ロガーはそのインターフェイスのすべての関数をフックし、ログを記録します。

以下に例を示します。

```cpp
STDAPI CoCreateInstance(
  REFCLSID rclsid,     //Class identifier (CLSID) of the object
  LPUNKNOWN pUnkOuter, //Pointer to controlling IUnknown
  CLSCTX dwClsContext, //Context for running executable code
  [iid] REFIID riid,   //Reference to the identifier of the interface
  [out] COM_INTERFACE_PTR * ppv
                       //Address of output variable that receives 
                       //the interface pointer requested in riid
);
```

この例で*riid*が、 \[iid\]修飾子。 これで、ポインターが返されるロガーに示します*ppv*で識別されるインターフェイスへの COM インターフェイス ポインター *riid*します。

次のように関数を宣言することもします。

```cpp
DDRESULT DirectDrawCreateClipper( DWORD dwFlags, [out] LPDIRECTDRAWCLIPPER *lplpDDClipper, IUnknown *pUnkOuter );
```

この例で、LPDIRECTDRAWCLIPPER がへのポインターとして定義された、 **IDirectDrawClipper**インターフェイス。 ロガーに返されるインターフェイスの種類を識別することができますので、 *lplpDDClipper*パラメーター必要はありません、 \[iid\]他のパラメーターのいずれかの修飾子。

 

 





