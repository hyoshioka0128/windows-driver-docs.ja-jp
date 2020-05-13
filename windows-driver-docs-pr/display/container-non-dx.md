---
title: DX 以外の Api のコンテナーサポート
description: DX 以外の Api はドライバーとカーネルをより直接やり取りする必要があるため、より複雑になることがあります。
ms.assetid: 6c4a6974-c67b-4710-80c6-48a5b378e088
ms.date: 05/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 34681000436867dae50f9c838e96412679138384
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235398"
---
# <a name="container-support-for-non-dx-apis"></a>DX 以外の Api のコンテナーサポート

Windows 10 では、DX 以外の Api に大きな影響を与える機能がいくつか追加されました。
1. 準仮想化 WDDM アダプター 
2. ユーザーは、自身を区別しないアプリケーションによって使用されるアダプターを制御できるようになりました
3. [ユニバーサルドライバー](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)は、新しい一連のデザインプリンシパルを導入します。

最新の Windows 10 機能との互換性を維持するには、次の点を変更する必要があります。

## <a name="driver-inf-modifications"></a>ドライバーの INF の変更
ドライバーは、Windows インストールの system32 および syswow64 サブディレクトリにバイナリをインストールするために、適切なレジストリの場所に DX 以外のランタイムを登録する必要があります。
インストール INF では、ドライバーは、グラフィックスアダプターのレジストリキーの次のサブキーに複数の値を定義できます。
- CopyToVmOverwrite
- CopyToVmWhenNewer
- CopyToVmOverwriteWow64
- CopyToVmWhenNewerWow64

前のサブキーによって system32 ディレクトリが変更されますが、後者のサブキーでは、syswow64 ディレクトリが変更されます。
サブキーの下にある各値の型は、REG_MULTI_SZ または REG_SZ である必要があります。 値の型が REG_MULTI_SZ 場合、値には最大2つの文字列が必要です。 これは、各値が stings のペアを定義することを意味します。2番目の文字列は空にすることができます。
ペアの最初の名前は、ドライバーストア内のファイルへのパスです。 パスは、ドライバーストアのルートを基準とした相対パスであり、サブディレクトリを含むことができます。
ペアの2番目の名前は、system32 または syswow64 ディレクトリに表示されるファイルの名前です。
2番目の名前は、パスを含まないファイル名だけにする必要があります。 2番目の名前が空の場合、ファイル名はドライバーストアと同じです (サブディレクトリは除く)。
これにより、ドライバーはホストドライバーストアとゲストに異なる名前を付けることができます。 

**Copytovmwhennewer**グラフィックアダプターレジストリサブキー **CopyToVmWhenNewerWow64**の下に一覧表示されるファイルは、"新しい" 条件を満たしている場合にのみ、対象のファイルを上書きします。

Windows 10 バージョン2004では、"新しい" 条件によって次の2つの情報が比較されます。
- [FileVersion](https://docs.microsoft.com/windows/desktop/api/verrsrc/ns-verrsrc-vs_fixedfileinfo)
- [最終書き込み時刻](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information)

コピー先のファイルの末尾が .dll または .exe の場合、最も重要な比較値として**FileVersion**が使用されます。この場合、最大バージョンは "新しい" と見なされます。

コピー先のファイルの末尾が .dll でも .exe でもない場合、または2つの**FileVersion**が等しい場合、 **lastwritetime**は、後の日付/時刻が "より新しい" と見なされる、最も重要度の高い比較値として使用されます。

2004より前のバージョンの Windows 10 では、"新しい" 条件によってファイルの[Changetime](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information)のみが比較されていました。

### <a name="example-1"></a>例 1:
INF [DDInstall] セクション  
HKR、"softgpukmd\CopyToVmOverwrite"、SoftGpuFiles、% REG_MULTI_SZ%、"Copytovm\ softgpufiles dll"、"softgpu2"  

ディレクティブによって、ソフトウェア (アダプター) キーにレジストリキーが作成されます。 "HKLM\SYSTEM\CurrentControlSet\Control\Class \\ {4d36e968-e325-11ce-bfc1-08002be10318} \\ \< number> \Copytovmoverwrite"、SoftGpuFiles = REG_MULTI_SZ、"copytovm"、"softgpu2"

OS は \< driverstorepath> \ Copytovm\ Softgpu%windir%\system32\softgpu2.dll dll を

### <a name="example-2"></a>例 2:
INF [DDInstall] セクション:  
HKR、"CopyToVmOverwrite"、SoftGpuFiles1、% REG_MULTI_SZ%、"softgpu1"、"softgpu .dll"  
HKR、"CopyToVmOverwrite"、SoftGpuFiles2、% REG_SZ%、"softgpu2"  

ディレクティブによって、ソフトウェア (アダプター) キーにレジストリキーが作成されます。  
"HKLM\SYSTEM\CurrentControlSet\Control\Class \\ {4d36e968-e325-11ce-bfc1-08002be10318} \\ \< number> \Copytovmoverwrite", SoftGpuFiles1 = REG_MULTI_SZ, "softgpu1", "softgpu .dll"  
"HKLM\SYSTEM\CurrentControlSet\Control\Class \\ {4d36e968-e325-11ce-bfc1-08002be10318} \\ \< number> \Copytovmoverwrite", SoftGpuFiles = REG_SZ, "softgpu2"  

OS は \< driverstorepath> \ softgpu1. dll を%windir%\system32\softgpu.dll にコピーし、 \< driverstorepath> を%windir%\system32\softgpu2.dll にコピーします。

### <a name="example-3"></a>例 3: 
INF [DDInstall] セクション:  
HKR、"CopyToVmOverwriteWow64"、SoftGpuFiles、% REG_MULTI_SZ%、"Subdir1\Subdir2\softgpu2wow64.dll"、"softgpu .dll"  

ディレクティブによって、ソフトウェア (アダプター) キーにレジストリキーが作成されます。  
"HKLM\SYSTEM\CurrentControlSet\Control\Class \\ {4d36e968-e325-11ce-bfc1-08002be10318} \\ \< number> \Copytovmoverwritewow64"、SoftGpuFiles = REG_MULTI_SZ、"Subdir1\Subdir2\softgpu2wow64.dll"、"softgpu .dll"  

OS は \< driverstorepath> \subdir1\subdir2\softgpu2wow64.dll を%windir%\syswow64\softgpu.dll にコピーします。

## <a name="driver-modifications-to-registry-and-file-paths"></a>レジストリおよびファイルパスに対するドライバーの変更
コンテナー内では、ドライバーストアは、通常と同じ標準的なパスには存在しません。
適切に調整されたパスを一貫して使用するには、レジストリとドライバーストアに[KMTQAITYPE_QUERYREGISTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ne-d3dkmthk-_kmtqueryadapterinfotype)と[D3DDDI_QUERYREGISTRY_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_queryregistry_info)[を使用して間接](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtqueryadapterinfo)的にアクセスする必要があります。

## <a name="honor-os-default-adapter-setting"></a>OS の既定のアダプター設定を優先する
既定のアダプターは、OS に格納されているユーザーの選択に従う必要があります。これには次のものが必要です。
1. Dxgi の[Idxgifactory:: EnumAdapters](https://docs.microsoft.com/windows/desktop/api/dxgi/nf-dxgi-idxgifactory-enumadapters)を通じてアダプターを列挙します。これは、ユーザーの選択に優先します。 アダプター0は、[ユーザーの設定](https://blogs.windows.com/windowsexperience/2018/02/07/announcing-windows-10-insider-preview-build-17093-pc/)に基づいて変更されます。
2. [D3DKMTEnumAdapters2](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtenumadapters2)によって実行されるアダプターの順序を DXGI のに一致させます。
アダプター id は、両方の列挙手法の間で LUID を相互に関連付けることによって、一致させることができます。
DXGI[は、Idxgiadapter:: GetDesc](https://docs.microsoft.com/windows/desktop/api/dxgi/nf-dxgi-idxgiadapter-getdesc)を介して LUID を返します。

## <a name="dchu-design-modifications"></a>DCHU のデザインの変更
では、可能な限り多くの[ユニバーサルドライバー](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)設計プリンシパルを使用します。これは、サポートされているデバイスによって異なる場合があります。

## <a name="d3dkmt-headers"></a>D3DKMT ヘッダー
前述のメソッドと型を含むヘッダーは、WDK で排他的に使用できるようにするのではなく、Windows 10 バージョン2004以降の Windows SDK で使用できます。

必要なヘッダーを明確に含めるためのオプションの1つに、次のようなものがあります。
その他のオプションも存在する場合があります。
```cpp
// Turn off NTSTATUS codes within windows.h, so that the more exhaustive ntstatus.h can be used.
#define UMDF_USING_NTSTATUS
#include <windows.h> // For the vast majority of Windows functionality
#include <winternl.h> // For NT_SUCCESS
#include <ntstatus.h> // For the most exhaustive list of NTSTATUS codes
#include <d3dkmthk.h> // For D3DKMT support
```
