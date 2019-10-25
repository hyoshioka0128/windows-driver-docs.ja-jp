---
title: マクロブロック制御コマンド
description: マクロブロック制御コマンド
ms.assetid: be70ec8f-1821-4075-b5e3-b7574fbe4e27
keywords:
- マクロは WDK DirectX VA、コマンドをブロックします
- DXVA_MBctrl_I_HostResidDiff_1
- DXVA_MBctrl_I_OffHostIDCT_1
- DXVA_MBctrl_P_HostResidDiff_1
- DXVA_MBctrl_P_OffHostIDCT_1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32fd7ef9f75f018eb0663fafff314a0a543dfb6e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840588"
---
# <a name="macroblock-control-commands"></a>マクロブロック制御コマンド


## <span id="ddk_macroblock_control_commands_gg"></span><span id="DDK_MACROBLOCK_CONTROL_COMMANDS_GG"></span>


圧縮された画像のデコード中の、デコードされた各マクロブロックの生成は、マクロブロックコントロールのコマンド構造によって管理されます。 *Dxva*ヘッダーファイルには、次の4つのマクロブロックコントロールコマンド構造が定義されています。

[**DXVA\_MBctrl\_I\_HostResidDiff\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_i_hostresiddiff_1)

[**DXVA\_MBctrl\_I\_OffHostIDCT\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_i_offhostidct_1)

[**DXVA\_MBctrl\_P\_HostResidDiff\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1)

[**DXVA\_MBctrl\_P\_OffHostIDCT\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_offhostidct_1)

*Dxva*で明示的に定義された構造体は、DirectX VA のマクロブロックコントロールコマンドに使用される一般的なデザインの特殊なケースです。 この汎用デザインの詳細については、「[汎用形式のマクロブロックコントロールのコマンド構造](generic-form-of-macroblock-control-command-structures.md)」を参照してください。

使用するマクロブロックコントロールのコマンド構造の選択は、デコードする画像の種類とデコードされる方法に基づいて行われます。 次の構造体のメンバーとフラグによって、画像の種類、デコードオプション、4つの DirectX VA マクロブロック制御構造のうち、どれが使用されるかが決まります。

-   **BbChromaFormat 内部**、、 **b絵文字 obmc**、 **bbPic4MVallowed Binpb**、 、および**Bmv\_RPS**のメンバーは、 [**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体です。

-   [**DXVA\_Configピクチャデコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)構造体の**bConfigResidDiffHost**メンバー。

-   *Hostresiddiff*フラグ (各マクロブロック制御構造の**wmbtype**メンバーのビット 10)。

次のセクションでは、これらの構造体のメンバーとフラグの値について説明します。

### <a name="span-iddxva_mbctrl_i_hostresiddiff_1spanspan-iddxva_mbctrl_i_hostresiddiff_1spanspan-iddxva_mbctrl_i_hostresiddiff_1spandxva_mbctrl_i_hostresiddiff_1"></a><span id="DXVA_MBctrl_I_HostResidDiff_1"></span><span id="dxva_mbctrl_i_hostresiddiff_1"></span><span id="DXVA_MBCTRL_I_HOSTRESIDDIFF_1"></span>DXVA\_MBctrl\_I\_HostResidDiff\_1

**DXVA\_MBctrl\_I\_HostResidDiff\_1**です。 次の構造体のメンバーとフラグは、指定された値と同じである必要があります。

-   **B絵文字**は、1 (画像内) に等しくなければなりません。

-   **bChromaFormat**は 1 (4:2:0 サンプリング) に等しくなければなりません。

-   *Hostresiddiff*は 1 (ホストベースの idct) と同じである必要があります。

-   **bConfigResidDiffHost**は 1 (ホストベースの残余差のデコード) に等しくなければなりません。

### <a name="span-iddxva_mbctrl_i_offhostidct_1spanspan-iddxva_mbctrl_i_offhostidct_1spanspan-iddxva_mbctrl_i_offhostidct_1spandxva_mbctrl_i_offhostidct_1"></a><span id="DXVA_MBctrl_I_OffHostIDCT_1"></span><span id="dxva_mbctrl_i_offhostidct_1"></span><span id="DXVA_MBCTRL_I_OFFHOSTIDCT_1"></span>DXVA\_MBctrl\_I\_OffHostIDCT\_1

[**DXVA\_MBctrl\_I\_OffHostIDCT\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_i_offhostidct_1)構造体は、4:2:0 サンプリングを使用して、ホスト間の残留差のデコードを無効にして、画像内で使用されます。 次の構造体のメンバーとフラグは、指定された値と同じである必要があります。

-   **B絵文字**は、1 (画像内) に等しくなければなりません。

-   **bChromaFormat**は 1 (4:2:0 サンプリング) に等しくなければなりません。

-   *Hostresiddiff*は0に等しくなければなりません (ホスト id を無効にする必要があります)。

-   **bConfigResidDiffHost**は0に等しくする必要があります (オフホストの残留差のデコード)。

### <a name="span-iddxva_mbctrl_p_hostresiddiff_1spanspan-iddxva_mbctrl_p_hostresiddiff_1spanspan-iddxva_mbctrl_p_hostresiddiff_1spandxva_mbctrl_p_hostresiddiff_1"></a><span id="DXVA_MBctrl_P_HostResidDiff_1"></span><span id="dxva_mbctrl_p_hostresiddiff_1"></span><span id="DXVA_MBCTRL_P_HOSTRESIDDIFF_1"></span>DXVA\_MBctrl\_P\_HostResidDiff\_1

[**DXVA\_MBctrl\_p\_HostResidDiff\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1)構造体は、ホストベースの残余差のデコードを含む p および B の画像に使用されます。 次のマクロブロックの制御プロセスは使用されません。 OBMC、PB 画像の B 部分のマクロブロックごとに4つのモーションベクターを使用し、モーションベクター参照の画像選択を使用します。

次の構造体のメンバーとフラグは、指定された値と同じである必要があります。

-   **bpicture** in は0に等しくなければなりません ( *P* picture と*B picture*または concealment motion vector for *I picture*)。

-   **bChromaFormat**は 1 (4:2:0 サンプリング) に等しくなければなりません。

-   *Hostresiddiff*は 1 (ホストベースの idct) と同じである必要があります。

-   **B絵文字 Obmc**は0に等しくなければなりません (obmc は使用されません)。

-   **Bmv\_RPS**は0に等しくなければなりません (モーションベクター参照画像の選択は使用されません)。

-   **BbPic4MVallowed Binpb**の少なくとも1つ (PB-フレームモーション補正が使用されていません) と (マクロブロックが使用されていない場合は、4つの前方参照モーションベクトル) が0になる必要があります。

-   **bConfigResidDiffHost**は 1 (ホストベースの残余差のデコード) に等しくなければなりません。

### <a name="span-iddxva_mbctrl_p_offhostidct_1spanspan-iddxva_mbctrl_p_offhostidct_1spanspan-iddxva_mbctrl_p_offhostidct_1spandxva_mbctrl_p_offhostidct_1"></a><span id="DXVA_MBctrl_P_OffHostIDCT_1"></span><span id="dxva_mbctrl_p_offhostidct_1"></span><span id="DXVA_MBCTRL_P_OFFHOSTIDCT_1"></span>DXVA\_MBctrl\_P\_OffHostIDCT\_1

[**DXVA\_MBctrl\_p\_OffHostIDCT\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_offhostidct_1)構造体は、p と B の画像に対して使用されます。4:2:0 サンプリングでは、ホストの残留差の不一致があります。 次のマクロブロックの制御プロセスは使用されません。 OBMC、PB 画像の B 部分のマクロブロックごとに4つのモーションベクターを使用し、モーションベクター参照の画像選択を使用します。

次の構造体のメンバーとフラグは、指定された値と同じである必要があります。

-   **DXVA\_ピクチャパラメーター**または concealment motion Vector in *I Pictures*) の**b** 。

-   **bChromaFormat**は 1 (4:2:0 サンプリング) に等しくなければなりません。

-   *Hostresiddiff*は0に等しくなければなりません (ホスト id を無効にする必要があります)。

-   **B絵文字 Obmc**は0に等しくなければなりません (obmc は使用されません)。

-   **Bmv\_RPS**は0に等しくなければなりません (モーションベクター参照画像の選択は使用されません)。

-   **BbPic4MVallowed Binpb**の少なくとも1つ (PB-フレームモーション補正が使用されていません) と (マクロブロックが使用されていない場合は、4つの前方参照モーションベクトル) が0になる必要があります。

-   **bConfigResidDiffHost**は0に等しくする必要があります (オフホストの残留差のデコード)。

 

 





