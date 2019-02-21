---
title: マクロ ブロック管理コマンド
description: マクロ ブロック管理コマンド
ms.assetid: be70ec8f-1821-4075-b5e3-b7574fbe4e27
keywords:
- WDK の DirectX va なので、コマンドをマクロ ブロック
- DXVA_MBctrl_I_HostResidDiff_1
- DXVA_MBctrl_I_OffHostIDCT_1
- DXVA_MBctrl_P_HostResidDiff_1
- DXVA_MBctrl_P_OffHostIDCT_1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46432e442e4c41bfe2db8a1a490b86f698689ebe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538034"
---
# <a name="macroblock-control-commands"></a>マクロ ブロック管理コマンド


## <span id="ddk_macroblock_control_commands_gg"></span><span id="DDK_MACROBLOCK_CONTROL_COMMANDS_GG"></span>


デコードされた各マクロ ブロックの圧縮された画像をデコード中に生成するマクロ ブロック コントロール コマンドの構造が適用されます。 定義された 4 つのマクロ ブロック コントロール コマンド構造がある、 *dxva.h*ヘッダー ファイル。

[**DXVA\_MBctrl\_I\_HostResidDiff\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563983)

[**DXVA\_MBctrl\_I\_OffHostIDCT\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563989)

[**DXVA\_MBctrl\_P\_HostResidDiff\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563993)

[**DXVA\_MBctrl\_P\_OffHostIDCT\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563997)

構造体で明示的に定義されている*dxva.h*マクロ ブロック コントロールのコマンドの DirectX 問い合わせください使用される汎用的なデザインの特殊なケース。 この汎用的な設計については、次を参照してください。[マクロ ブロック コントロール コマンド構造の汎用フォーム](generic-form-of-macroblock-control-command-structures.md)します。

使用できるマクロ ブロック コントロール コマンド構造体の選択はデコードする画像の種類とデコードする方法に基づいています。 次の構造体のメンバーとフラグ オプション、および 4 つの DirectX VA マクロ ブロックの制御構造のどちらを使用するデコードを画像の種類に決定します。

-   **BPicIntra**、 **bChromaFormat**、 **bPicOBMC**、 **bPicBinPB**、 **bPic4MVallowed**と**bMV\_RPS**のメンバー、 [ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)構造体。

-   **BConfigResidDiffHost**のメンバー、 [ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)構造体。

-   *HostResidDiff*フラグ (の 10 ビット、 **wMBtype**各マクロ ブロック コントロールの構造体のメンバー)。

これらの構造体のメンバーとフラグの値は、次のセクションに表示されます。

### <a name="span-iddxvambctrlihostresiddiff1spanspan-iddxvambctrlihostresiddiff1spanspan-iddxvambctrlihostresiddiff1spandxvambctrlihostresiddiff1"></a><span id="DXVA_MBctrl_I_HostResidDiff_1"></span><span id="dxva_mbctrl_i_hostresiddiff_1"></span><span id="DXVA_MBCTRL_I_HOSTRESIDDIFF_1"></span>DXVA\_MBctrl\_I\_HostResidDiff\_1

**DXVA\_MBctrl\_は\_HostResidDiff\_1**します。 次の構造体のメンバーとフラグ値でなければなりません。

-   **bPicIntra** 1 (内の画像) でなければなりません。

-   **bChromaFormat** 1 (4:2:0 サンプリング) に等しい必要があります。

-   *HostResidDiff* (ホスト ベース IDCT) を 1 に等しい必要があります。

-   **bConfigResidDiffHost** (残存違いのホストベースのデコード) 1 でなければなりません。

### <a name="span-iddxvambctrlioffhostidct1spanspan-iddxvambctrlioffhostidct1spanspan-iddxvambctrlioffhostidct1spandxvambctrlioffhostidct1"></a><span id="DXVA_MBctrl_I_OffHostIDCT_1"></span><span id="dxva_mbctrl_i_offhostidct_1"></span><span id="DXVA_MBCTRL_I_OFFHOSTIDCT_1"></span>DXVA\_MBctrl\_I\_OffHostIDCT\_1

[ **DXVA\_MBctrl\_は\_OffHostIDCT\_1** ](https://msdn.microsoft.com/library/windows/hardware/ff563989)構造が 4 内の画像の使用: 2:0 サンプリング オフホスト残存相違点がありますデコードします。 次の構造体のメンバーとフラグ値でなければなりません。

-   **bPicIntra** 1 (内の画像) でなければなりません。

-   **bChromaFormat** 1 (4:2:0 サンプリング) に等しい必要があります。

-   *HostResidDiff* 0 (オフホスト IDCT) を等しく必要があります。

-   **bConfigResidDiffHost** 0 (オフホスト残存違いデコード) と等しく必要があります。

### <a name="span-iddxvambctrlphostresiddiff1spanspan-iddxvambctrlphostresiddiff1spanspan-iddxvambctrlphostresiddiff1spandxvambctrlphostresiddiff1"></a><span id="DXVA_MBctrl_P_HostResidDiff_1"></span><span id="dxva_mbctrl_p_hostresiddiff_1"></span><span id="DXVA_MBCTRL_P_HOSTRESIDDIFF_1"></span>DXVA\_MBctrl\_P\_HostResidDiff\_1

[ **DXVA\_MBctrl\_P\_HostResidDiff\_1** ](https://msdn.microsoft.com/library/windows/hardware/ff563993)残存違いのホスト ベースのデコードの P と B の画像の構造を使用します。 次のマクロ ブロック制御プロセスは使用されません。OBMC、PB 図の B 部分のマクロ ブロックごとの 4 つの動きベクトルの使用および動きベクトルの使用は、画像の選択を参照します。

次の構造体のメンバーとフラグ値でなければなりません。

-   **bPicIntra** 0 と等しく必要があります (のデコード*P 画像*と*B 画像*またはで動きベクトルの補填*画像は*)。

-   **bChromaFormat** 1 (4:2:0 サンプリング) に等しい必要があります。

-   *HostResidDiff* (ホスト ベース IDCT) を 1 に等しい必要があります。

-   **bPicOBMC** 0 (OBMC 使用されません) を等しく必要があります。

-   **bMV\_RPS** 0 (動きベクトルの参照を画像の選択使用されません) を等しく必要があります。

-   少なくとも 1 つの**bPicBinPB** PB フレーム モーション報酬が使用されません (B の画像) と**bPic4MVallowed** (未使用のマクロ ブロックあたり 4 つの前方参照モーション ベクトル) は 0 と等しく必要があります。

-   **bConfigResidDiffHost** (残存違いのホストベースのデコード) 1 でなければなりません。

### <a name="span-iddxvambctrlpoffhostidct1spanspan-iddxvambctrlpoffhostidct1spanspan-iddxvambctrlpoffhostidct1spandxvambctrlpoffhostidct1"></a><span id="DXVA_MBctrl_P_OffHostIDCT_1"></span><span id="dxva_mbctrl_p_offhostidct_1"></span><span id="DXVA_MBCTRL_P_OFFHOSTIDCT_1"></span>DXVA\_MBctrl\_P\_OffHostIDCT\_1

[ **DXVA\_MBctrl\_P\_OffHostIDCT\_1** ](https://msdn.microsoft.com/library/windows/hardware/ff563997)構造が 4 で画像を P と B の使用: 2:0 サンプリング オフホスト残存相違点がありますデコードします。 次のマクロ ブロック制御プロセスは使用されません。OBMC、PB 図の B 部分のマクロ ブロックごとの 4 つの動きベクトルの使用および動きベクトルの使用は、画像の選択を参照します。

次の構造体のメンバーとフラグ値でなければなりません。

-   **bPicIntra**のメンバー、 **DXVA\_PictureParameters**またはで動きベクトルの補填*画像は*)。

-   **bChromaFormat** 1 (4:2:0 サンプリング) に等しい必要があります。

-   *HostResidDiff* 0 (オフホスト IDCT) を等しく必要があります。

-   **bPicOBMC** 0 (OBMC 使用されません) を等しく必要があります。

-   **bMV\_RPS** 0 (動きベクトルの参照を画像の選択使用されません) を等しく必要があります。

-   少なくとも 1 つの**bPicBinPB** PB フレーム モーション報酬が使用されません (B の画像) と**bPic4MVallowed** (未使用のマクロ ブロックあたり 4 つの前方参照モーション ベクトル) は 0 と等しく必要があります。

-   **bConfigResidDiffHost** 0 (オフホスト残存違いデコード) と等しく必要があります。

 

 





