---
title: DX された Api 用のコンテナーのサポート
description: 非 DX Api 対話する必要があるドライバーやカーネルを直接より複雑で複数公開されているため
ms.assetid: 6c4a6974-c67b-4710-80c6-48a5b378e088
ms.date: 04/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: eed3c747bb5ff1228d1841cfad59fad9b89b219c
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902320"
---
# <a name="container-support-for-non-dx-apis"></a>DX された Api 用のコンテナーのサポート

Windows 10 では、非-DX Api、および下位 WDDM アーキテクチャの詳細に依存している大きな影響を与えるいくつかの機能を追加します。
1. 準仮想化 WDDM アダプター 
2. ユーザーに自身を識別しないアプリケーションで使用するアダプターを制御があるようになりました
3. [ユニバーサル ドライバー](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)デザインのプリンシパルの新しいセットが導入されています

最新の Windows 10 の機能との互換性を維持するには、次の変更が必要です。

レジストリとドライバー ストアはを介して間接的にアクセスする必要があります[D3DKMTQueryAdapterInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtqueryadapterinfo)で[KMTQAITYPE_QUERYREGISTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ne-d3dkmthk-_kmtqueryadapterinfotype)、および[D3DDDI_QUERYREGISTRY_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_queryregistry_info)します。

既定のアダプターが必要ですが、ユーザーの選択を受け付ける必要があります。
1. DXGI のを通じてアダプターを列挙する[IDXGIFactory::EnumAdapters](https://docs.microsoft.com/windows/desktop/api/dxgi/nf-dxgi-idxgifactory-enumadapters)DXGI はユーザーの選択を優先します。 0 のアダプターの変更に基づいて、[ユーザーの設定](https://blogs.windows.com/windowsexperience/2018/02/07/announcing-windows-10-insider-preview-build-17093-pc/)します。
2. によって得られたアダプターの順序と一致して[D3DKMTEnumAdapters2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtenumadapters2) DXGI にします。
列挙型の両方の手法の間で LUID を関連付けることによってアダプターの id 照合できます。
DXGI 返しますを通じてその LUID [IDXGIAdapter::GetDesc](https://docs.microsoft.com/windows/desktop/api/dxgi/nf-dxgi-idxgiadapter-getdesc)します。

できる限り、異なる場合がありますサポートされている正確なデバイスに基づく多くユニバーサル ドライバーの設計方針を優先します。
