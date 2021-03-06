---
title: エクスポート ドライバーの作成
description: エクスポート ドライバーの作成
ms.assetid: 60ce7d0d-0eab-4af6-890a-45ab206816aa
keywords:
- ドライバー WDK カーネルをエクスポートします。
- ロードは、ドライバー WDK カーネルをエクスポートします。
- ドライバー関数のエクスポートをインポートします。
- モジュール定義ファイルの WDK カーネル
- .def ファイル
- def ファイル
- カーネル モード ドライバー WDK、ドライバーをエクスポートします。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11de78c3df6d16cc5f485a120e12215ce561115c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377168"
---
# <a name="creating-export-drivers"></a>エクスポート ドライバーの作成





通常、Microsoft Windows ドライバーは、ポート/ミニポート ドライバーのペア、またはクラス/miniclass ドライバー ペアなどのコンポーネントのペアとして定義されます。 通常、Microsoft は、ハードウェアに依存しないクラスまたはポートのドライバーを提供し、仕入先がハードウェア依存の miniclass またはミニポート ドライバーを提供します。

エクスポートのカーネル モード ドライバーは特に適して、エクスポートのドライバーが読み込むことができるその他のさまざまなカーネル モード DLL のためのスタックとハードウェアの特性を基になるから独立しているドライバーのペアの一部を実装します。特定のハードウェアまたはデバイス スタック固有のコンポーネント。 Microsoft では、このカテゴリに分類されると共に、Windows オペレーティング システムのいくつかのドライバーが付属しています。 たとえば、SCSI ポート ドライバー、テープのクラス ドライバーは、IDE コント ローラーのドライバーは、他のドライバーによって読み込まれるすべてのシステム提供のエクスポート ドライバーです。

エクスポートされたドライバーは、完全なカーネル モード ドライバーの特性の多くがありません。 エクスポートされたドライバーには、ディスパッチ テーブルはありません、ドライバー スタック内の場所がないおよびシステム サービスとしてそれを定義するサービス コントロール マネージャーのデータベース内のエントリはありません。 エクスポート、ドライバーが、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチンが、その**DriverEntry**ルーチンが呼び出されない。 (ルーチンは、ビルド スクリプトの要件を満たすためにスタブのみです)。

エクスポートされたドライバーはディスパッチ テーブルを持たないときに、標準のドライバーにディスパッチ ルーチンを供給できることに注意してください。 標準のドライバーでは、独自のディスパッチ テーブルにディスパッチ ルーチンを挿入します。

標準のドライバーは、ドライバーのエクスポートにも機能します。 両方の方法で関数へのドライバーの場合、エクスポート ドライバーとしてビルドして、正規のドライバーとして読み込ま 必要があります。

### <a name="building-an-export-driver"></a>エクスポートされたドライバーの構築

エクスポートのドライバーとしてドライバーをビルドするには、ドライバーのソース ファイルでいくつかのビルド ユーティリティ マクロを定義する必要があります。

最初に、適切な値を割り当てる必要があります、 **TARGETTYPE**マクロは、次のようにします。

```cpp
TARGETTYPE=EXPORT_DRIVER
```

使用してモジュール定義 (.def) ファイルを指定する必要がありますも、 **DLLDEF**マクロ。 次に、例を示します。

```cpp
DLLDEF="c:\project\driver.def"
```

モジュール定義ファイルでは、コンパイラとリンカーが他の情報と共にエクスポートしたルーチンの一覧を提供します。 モジュール定義ファイルの詳細については、Microsoft Visual C のドキュメントを参照してください。

ユーザー モード DLL のビルドで採用されているビルド ユーティリティ マクロの多くは、カーネル モード DLL のビルド時に使用できません。 

たとえば、カーネル モード DLL のエントリ ポイントは、常に**DllInitialize**します。 システムは、DLL が読み込まれた後にすぐに、カーネル モード DLL の DllInitialize ルーチンを呼び出します。 エクスポートのドライバーを提供する必要があります**DllInitialize**ルーチン。 使用することができます、 **DllInitialize**ルーチンを取得するか、DLL 内の他のルーチンで必要なリソースを初期化します。 

使用して、エントリ ポイントを指定することはできません、 **DLLENTRY**マクロ。 

```cpp
NTSTATUS DllInitialize(
  _In_ PUNICODE_STRING RegistryPath
);
```
RegistryPath は DLL のレジストリ キーへのパスを指定する、カウント対象の Unicode 文字列へのポインター **HKEY_LOCAL_MACHINE\CurrentControlSet\Services\DllName**します。 DLL のルーチンでは、DLL に固有の情報を格納するのに、このキーを使用できます。 RegistryPath によって指し示されるバッファーが 1 回解放**DllInitialize**が終了します。 そのため、DLL を行った場合、キーの使用**DllInitialize**キー名を複製する必要があります。 


ビルド プロセスには、.lib 拡張子を持つエクスポート ライブラリと .sys 拡張子を持つエクスポート ドライバーが生成されます。

### <a name="importing-functions-from-an-export-driver"></a>エクスポートされたドライバーから関数をインポートします。

エクスポート ドライバーによってエクスポートされる関数をインポートするには、DECLSPEC を使用して関数を宣言しなければなりません\_Ntdef.h で定義されているインポート マクロ。 例:

```cpp
DECLSPEC_IMPORT int LoadPrinterDriver (int arg1); 
```

このマクロに解決する **\_ \_declspec**(dllimport) ストレージ クラスのこれらのプラットフォームでの宣言に必要な場合、これらのプラットフォーム上の何も必要ない場合。

エクスポート ドライバーでは、エクスポートする関数を DECLSPEC と共に宣言する必要があります\_マクロをエクスポートします。 このマクロに解決する **\_ \_declspec**(dllexport) ストレージ クラスのこれらのプラットフォームでの宣言に必要な場合、これらのプラットフォーム上の何も必要ない場合。 エクスポートされたドライバーが標準のドライバーにディスパッチ ルーチンを提供している場合、ルーチンをエクスポートするはありません。

### <a name="loading-and-unloading-an-export-driver"></a>読み込みとエクスポート、ドライバーをアンロード

%Windir% でエクスポート ドライバーをインストールする必要があります\\System32\\ドライバー ディレクトリ。 Windows 2000 以降、オペレーティング システムは、エクスポート ドライバーの関数は、他のドライバーがインポートされている回数を示す参照カウントを保持します。 システム デクリメント インポート ドライバーのいずれかがアンロードされるたびに、このカウントします。 参照カウントがゼロになる、システムは、エクスポートのドライバーをアンロードします。 ただし、エクスポートのドライバーを標準のエントリ ポイントが含まれて、ルーチンをアンロードする必要があります**DllInitialize**と**DllUnload**、またはオペレーティング システムはこの参照カウントのメカニズムをアクティブになりません。

システムは、DLL をアンロードしたときに、カーネル モード DLL の DllUnload ルーチンを呼び出します。

```cpp
NTSTATUS DllUnload(void);
```
エクスポートのドライバーでは、DllUnload ルーチンを提供する必要があります。 DllUnload ルーチンを使用して、DLL のルーチンで使用されるリソースを解放することができます。 








