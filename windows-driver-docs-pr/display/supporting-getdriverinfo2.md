---
title: GetDriverInfo2 のサポート
description: GetDriverInfo2 のサポート
ms.assetid: 5e2dd363-9e72-4674-940e-8b4f06f6eb14
keywords:
- DirectX 8.0 リリースノート WDK Windows 2000 display、GetDriverInfo2
- GetDriverInfo2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7aa383699431b8a625772de198ffef7d94325ee1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825624"
---
# <a name="supporting-getdriverinfo2"></a>GetDriverInfo2 のサポート


## <span id="ddk_supporting_getdriverinfo2_gg"></span><span id="DDK_SUPPORTING_GETDRIVERINFO2_GG"></span>


DirectX 8.0 DDI では、ドライバーに情報を照会するための新しいメカニズムが導入されています。 このメカニズムにより、既存の[**Ddgetdriverinfo**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)エントリポイントが拡張され、ドライバーからの追加情報が照会されます。 現時点では、このメカニズムは DX8 スタイルの D3D キャップのクエリにのみ使用されます。

**GetDriverInfo2**のメカニズムが必要な理由については、以下をお読みください **。  ** D3DCAP8 構造体を返すことによって、ドライバーが処理する新しい**Getdriverinfo** GUID を単に定義することをお勧めします。 次の段落で導入された**GetDriverInfo2**は、directx 8.0 レベルの機能を有効にするために Windows オペレーティングシステムに必要な変更を最小限に抑え、directx 8.0 ランタイムを実際に再配布できるようにするためのメカニズムです。

 

この**Getdriverinfo**の拡張機能は、GUID\_GetDriverInfo2 を持つ*ddgetdriverinfo*呼び出しの形式を受け取ります。 この GUID を持つ*Ddgetdriverinfo*呼び出しがドライバーによって受信された場合、要求されている情報を確認するには、 [**DD\_getdriverinfodata**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)データ構造の**lpvdata**フィールドで渡されたデータ構造を確認する必要があります。 以下で説明するように、 **Lpvdata**は、 [**dd\_GETDRIVERINFO2DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getdriverinfo2data)または[**dd\_STEREOMODE**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_stereomode)構造体を指すことができます。

Guid\_GetDriverInfo2 は guid\_DDStereoMode と同じ guid 値です。 ドライバーが GUID\_DDStereoMode を処理しない場合、これは問題ではありません。 ただし、DirectX 8.0 ドライバーが GUID\_DDStereoMode を処理する場合、GUID\_GetDriverInfo2 (GUID\_DDStereoMode) を持つ*Ddgetdriverinfo*の呼び出しが行われると、ランタイムは DD の**dwHeight**フィールドを設定することに注意してください\_STEREOMODE 構造体を特別な値 D3DGDI2\_マジックにします。 このフィールドは、DD\_GETDRIVERINFO2DATA 構造体の**Dwmagic**フィールドに対応しています。 そのため、 **Lpvdata**ポインターを、DD\_STEREOMODE 構造体へのポインター、または DD\_GETDRIVERINFO2DATA 構造体へのポインターにキャストし、対応するフィールド (**DwHeight**または**dwmagic**) の値を確認します。値 D3DGDI2\_マジックの場合、ステレオモード機能を決定する呼び出しと Direct3D 8.0 機能の要求を区別できます。

ドライバーが**GetDriverInfo2**の呼び出しであると判断したら、ランタイムによって要求されている情報の種類を判断する必要があります。 この型は、DD\_GETDRIVERINFO2DATA データ構造体の**dwType**フィールドに含まれています。

最後に、指定したバッファーに要求されたデータをコピーします。 DD\_GETDRIVERINFODATA データ構造の**Lpvdata**フィールドは、要求されたデータのコピー先のバッファーを指していることに注意する必要があります。 また、 **Lpvdata**は、DD\_GETDRIVERINFO2DATA 構造体も指します。 これは、ドライバーによって返されるデータが、DD\_GETDRIVERINFO2DATA 構造体を上書きすることを意味します (したがって、DD\_GETDRIVERINFO2DATA 構造体がバッファーの最初のいくつかの Dword を占有することを意味します)。

**GetDriverInfo2**で呼び出されるようにし、DirectX 8.0 の機能を報告するには、GetDriverInfo2 HALINFO 構造体[ **\_** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)の**DWFLAGS**フィールドに新しいフラグ ddhalinfo\_を設定する必要があります。ドライバー。 このフラグが設定されていない場合、ランタイムはドライバーへの**GetDriverInfo2**呼び出しを送信せず、ドライバーは DirectX 8.0 レベルのドライバーとして認識されません。

ランタイムは、\_type\_DXVERSION の**GetDriverInfo2**を使用して、アプリケーションによって使用されている現在の DX ランタイムバージョンをドライバーに通知します。 ランタイムは、dd\_GETDRIVERINFODATA の**Lpvdata**フィールド内の[**DD\_dxversion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_dxversion)構造体へのポインターを提供します。

 

 





