---
title: DX された Api 用のコンテナーのサポート
description: 非 DX Api 対話する必要があるドライバーやカーネルを直接より複雑で複数公開されているため
ms.assetid: 6c4a6974-c67b-4710-80c6-48a5b378e088
ms.date: 05/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: ed5ff1d1438f20c225076c608d6c7a3e264d5b3b
ms.sourcegitcommit: 0c364a5c4947fcfe815de5fb57237c3e36b3ae20
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65701993"
---
# <a name="container-support-for-non-dx-apis"></a>DX された Api 用のコンテナーのサポート

Windows 10 では、非-DX Api、および下位 WDDM アーキテクチャの詳細に依存している大きな影響を与えるいくつかの機能を追加します。
1. 準仮想化 WDDM アダプター 
2. ユーザーに自身を識別しないアプリケーションで使用するアダプターを制御があるようになりました
3. [ユニバーサル ドライバー](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)デザインのプリンシパルの新しいセットが導入されています

最新の Windows 10 の機能との互換性を維持するには、次の変更が必要です。

## <a name="driver-inf-modifications"></a>ドライバーの INF 変更
ドライバーは、Windows インストールの system32 と syswow64 サブディレクトリに、バイナリをインストールする適切なレジストリの場所に非 DX ランタイムを登録する必要があります。
INF のインストールでは、ドライバーはグラフィックス アダプターのレジストリ キーのサブキー以下で複数の値を定義できます。
- CopyToVmOverwrite
- CopyToVmWhenNewer
- CopyToVmOverwriteWow64
- CopyToVmWhenNewerWow64

以前の下位のキーは、後者のサブ キー syswow64 ディレクトリを変更するときに、system32 ディレクトリを変更します。
__新しい__は、ファイルの比較することで定義されている[ChangeTime](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information)します。
サブキーの下には、各値型は、REG_MULTI_SZ または REG_SZ である必要があります。 REG_MULTI_SZ の場合は、値の型がある最大 2 つの文字列値。 これは、ため、各値が、2 番目の文字列が空にすること、文字列のペアを定義します。
ペアの最初の名前は、ドライバー ストア内のファイルへのパスです。 パスは、ドライバー ストアのルートに対する相対パスです、ディレクトリのサブディレクトリを含めることができます。
ペアの 2 つ目の名前は、system32 または syswow64 ディレクトリに表示するファイルの名前です。
2 番目の名前は、ファイル名のみ、パスを含まないである必要があります。 2 番目の名前が空の場合、ファイル名は (サブディレクトリを除く)、ドライバー ストアと同じになります。
これにより、ゲストおよびホストのドライバー ストアで異なる名前に、ドライバーができます。 

### <a name="example-1"></a>例 1:
[サービスのインストール セクション] INF セクション  
HKR、SoftGpuFiles、"softgpukmd\CopyToVmOverwrite"%reg_multi_sz"CopyToVm\softgpu1.dll"%"softgpu2.dll"  

ディレクティブは、サービス キーのレジストリ キーを作成します。"HKLM\SYSTEM\CurrentControlSet\Services\softgpukmd\CopyToVmOverwrite", SoftGpuFiles = REG_MULTI_SZ, "CopyToVm\softgpu1.dll", "softgpu2.dll"

OS はコピー \<DriverStorePath > %windir%\system32\softgpu2.dll に \CopyToVm\softgpu1.dll

### <a name="example-2"></a>例 2:
INF [DDInstall] セクションの内容:  
HKR、"CopyToVmOverwrite"、SoftGpuFiles1、REG_MULTI_SZ %、"softgpu1.dll"、"softgpu.dll"  
HKR、"CopyToVmOverwrite"、SoftGpuFiles2、REG_SZ %、"softgpu2.dll"  

ディレクティブはソフトウェア (アダプター) キーのレジストリ キーを作成します。  
"HKLM\SYSTEM\CurrentControlSet\Control\Class\\{4d36e968-e325-11ce-bfc1-08002be10318}\\\<数 > \CopyToVmOverwrite"、SoftGpuFiles1 = REG_MULTI_SZ、"softgpu1.dll"、"softgpu.dll"  
"HKLM\SYSTEM\CurrentControlSet\Control\Class\\{4d36e968-e325-11ce-bfc1-08002be10318}\\\<数 > \CopyToVmOverwrite"、SoftGpuFiles = REG_SZ"softgpu2.dll"  

OS はコピー \<DriverStorePath > %windir%\system32\softgpu.dll に \softgpu1.dll と\<DriverStorePath > %windir%\system32\softgpu2.dll に \softgpu2.dll

### <a name="example-3"></a>例 3: 
INF [DDInstall] セクションの内容:  
HKR、"CopyToVmOverwriteWow64"、SoftGpuFiles、%reg_multi_sz"Subdir1\Subdir2\softgpu2wow64.dll"%"softgpu.dll"  

ディレクティブはソフトウェア (アダプター) キーのレジストリ キーを作成します。  
"HKLM\SYSTEM\CurrentControlSet\Control\Class\\{4d36e968-e325-11ce-bfc1-08002be10318}\\\<数 > \CopyToVmOverwriteWow64"、SoftGpuFiles REG_MULTI_SZ、"Subdir1\Subdir2\softgpu2wow64.dll"="softgpu.dll"  

OS はコピー \<DriverStorePath > %windir%\syswow64\softgpu.dll に \Subdir1\Subdir2\softgpu2wow64.dll

## <a name="driver-modifications-to-registry-and-file-paths"></a>レジストリとファイル パスにドライバーの変更
コンテナー内では通常、ドライバー ストアは一貫して同じ正規パスに配置されているありません。
一貫して正しく調整済みのパスを使用して、レジストリとドライバー ストアをを介して間接的にアクセスする必要が[D3DKMTQueryAdapterInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtqueryadapterinfo)で[KMTQAITYPE_QUERYREGISTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ne-d3dkmthk-_kmtqueryadapterinfotype)、および[D3DDDI_QUERYREGISTRY_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_queryregistry_info)します。

## <a name="honor-os-default-adapter-setting"></a>OS の既定のアダプターの設定は無視されます。
既定のアダプターは、必要とすると、OS に格納されているユーザーの選択を受け付ける必要があります。
1. DXGI のを通じてアダプターを列挙する[IDXGIFactory::EnumAdapters](https://docs.microsoft.com/windows/desktop/api/dxgi/nf-dxgi-idxgifactory-enumadapters)DXGI はユーザーの選択を優先します。 0 のアダプターの変更に基づいて、[ユーザーの設定](https://blogs.windows.com/windowsexperience/2018/02/07/announcing-windows-10-insider-preview-build-17093-pc/)します。
2. によって得られたアダプターの順序と一致して[D3DKMTEnumAdapters2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtenumadapters2) DXGI にします。
列挙型の両方の手法の間で LUID を関連付けることによってアダプターの id 照合できます。
DXGI 返しますを通じてその LUID [IDXGIAdapter::GetDesc](https://docs.microsoft.com/windows/desktop/api/dxgi/nf-dxgi-idxgiadapter-getdesc)します。

## <a name="dchu-design-modifications"></a>DCHU デザインの変更
できるだけ従う[ユニバーサル ドライバー](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)限り、異なる場合があります、正確なデバイスがサポートされているに基づいてのプリンシパルを設計します。

## <a name="wdk-dependency"></a>WDK の依存関係

前述のメソッドと型の多くは、WDK は、ドライバーをビルドするために使用でのみ使用できます。
これは、DX 以外の Api は、Windows SDK だけに依存が以前の Microsoft のヘッダーでは、組織の不幸不注意です。
それほど面倒のない DX Api WDK またはランタイムまたはローダー コンポーネントを WDK の内訳をローカライズする場合は、マイクロソフトは、WDK の依存関係を効果的に切断 DX API プロジェクトのアクセス許可。
Microsoft のパブリックのドキュメントを使用して、バイナリ互換性のある型とそれをプロジェクトに関数の宣言を作成して WDK の依存関係を解消することができます。
これらの型名は、他のユーザーが意図的に DX API プロジェクトで、WDK をで活用する場合、名前の競合を回避するために、Microsoft で使用されるものと同じですがあります。

