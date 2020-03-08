---
title: ドライバーのロード時期の決定方法
description: ドライバーのロード時期の決定方法
ms.assetid: fe0f27e4-84d4-483e-8b4e-69c39ae332de
keywords:
- フィルタードライバー WDK ファイルシステム、ドライバーの読み込み
- ファイルシステムフィルタードライバー WDK、ドライバーの読み込み
- WDK ファイルシステムの読み込み中のドライバー
- ドライバー WDK ファイルシステムを読み込んでいます
- ドライバーの開始の種類 WDK ファイルシステム
- WDK ファイルシステムの種類の開始
- 読み込み順序グループ WDK ファイルシステム
- SERVICE_BOOT_START
- SERVICE_SYSTEM_START
- SERVICE_AUTO_START
- SERVICE_DEMAND_START
- SERVICE_DISABLED
- ブートドライバー WDK ファイルシステム
- ブート開始ドライバー WDK ファイルシステム
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 101f4ddb8d7fa6f255808551bbc91738ea1c974d
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910445"
---
# <a name="what-determines-when-a-driver-is-loaded"></a>ドライバーのロード時期の決定方法

> [!NOTE]
> 最適な信頼性とパフォーマンスを得るには、従来のファイルシステムフィルタードライバーではなく、フィルターマネージャーをサポートする[ファイルシステムミニフィルタードライバー](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-concepts)を使用します。 レガシドライバーをミニフィルタードライバーに移植する方法については、「[レガシフィルタードライバーを移植するためのガイドライン](guidelines-for-porting-legacy-filter-drivers.md)」を参照してください。

システムのブートシーケンス中にファイルシステムドライバーが読み込まれるタイミングと方法を調べる前に、ドライバーの開始の種類と読み込み順序のグループについて理解しておく必要があります。

## <a name="driver-start-types"></a>ドライバーの開始の種類

カーネルモードドライバーの開始の*種類*では、ドライバーがシステムの起動時または起動後に読み込まれるかどうかを指定します。 次の5つの開始の種類があります。

- SERVICE_BOOT_START (0x00000000)  
  オペレーティングシステム (OS) ローダーによって開始されたドライバーを示します。 ファイルシステムフィルタードライバーは、通常、この開始の種類または SERVICE_DEMAND_START を使用します。 Microsoft Windows XP およびそれ以降のシステムでは、新しい[ファイルシステムフィルターの読み込み順序グループ](load-order-groups-for-file-system-filter-drivers.md)を利用するために、フィルターでこのスタートアップの種類を使用する必要があります。

- SERVICE_SYSTEM_START (0x00000001)  
  OS の初期化中にドライバーが開始されたことを示します。 この開始の種類は、ファイルシステムレコグナイザーによって使用されます。 "SERVICE_DISABLED" の下に一覧表示されているファイルシステムを除き、ファイルシステム (ネットワークファイルシステムコンポーネントを含む) は、通常、この種類の開始または SERVICE_DEMAND_START を使用します。 このスタートアップの種類は、システムの初期化中に列挙され、システムの読み込みには必要ない PnP デバイスのデバイスドライバーによっても使用されます。

- SERVICE_AUTO_START (0x00000002)  
  システムの起動時にサービスコントロールマネージャーによって開始されたドライバーを示します。 ほとんど使用されません。

- SERVICE_DEMAND_START (0x00000003)  
  PnP マネージャー (デバイスドライバーの場合) またはサービスコントロールマネージャー (ファイルシステムとファイルシステムフィルタードライバーの場合) のいずれかによって、要求時にドライバーが開始されたことを示します。

- SERVICE_DISABLED (0x00000004)  
  OS ローダー、サービスコントロールマネージャー、または PnP マネージャーによって開始されていないドライバーを示します。 ファイルシステムレコグナイザー (ブートファイルシステムの場合を除く) または (EFS の場合) 別のファイルシステムによって読み込まれるファイルシステムによって使用されます。 このようなファイルシステムには、CDFS、EFS、FastFat、NTFS、UDF などがあります。 デバッグ中にドライバーを一時的に無効にするためにも使用されます。

## <a name="specifying-start-type"></a>指定 (開始の種類を)

ドライバーライターは、次のいずれかの方法で、インストール時にドライバーの開始の種類を指定できます。

- ドライバーの INF ファイルの[**addservice**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)ディレクティブによっ*て参照さ*れている、 **starttype**エントリの開始の種類を指定します。 この方法については、「ServiceInstall」セクションを参照してください。

- ユーザーモードインストールプログラムから**CreateService**または**ChangeServiceConfig**を呼び出すときに、 *dwstarttype*パラメーターに必要な開始の種類を渡します。 このメソッドについては、Microsoft Windows SDK のドキュメントの**CreateService**と**ChangeServiceConfig**のリファレンスエントリを参照してください。

## <a name="driver-load-order-groups"></a>ドライバーの読み込み順序グループ

SERVICE_BOOT_START および SERVICE_SYSTEM_START の開始の種類では、ドライバーが読み込まれる相対的な順序は、各ドライバーの*読み込み順序グループ*によって指定されます。

開始の種類が SERVICE_BOOT_START のドライバーは、*ブート (ブート開始) ドライバー*と呼ばれます。 Microsoft Windows 2000 以前のシステムでは、ブートドライバーであるほとんどのフィルターは "フィルター" グループに属しています。 Microsoft Windows XP 以降のシステムでは、通常、ブートドライバーであるフィルターは、新しい FSFilter の読み込み順序グループの1つに属しています。 これらの負荷順序グループの詳細については、「[ファイルシステムフィルタードライバーの読み込み順序グループ](load-order-groups-for-file-system-filter-drivers.md)」を参照してください。

開始の種類が SERVICE_SYSTEM_START であるドライバーも、それらが属する読み込み順序グループの順序で読み込まれます。 ただし、すべてのブートドライバーが読み込まれるまで、システム開始ドライバーは読み込まれません。

> [!NOTE]
> 開始の種類が SERVICE_AUTO_START、SERVICE_DEMAND_START、または SERVICE_DISABLED であるドライバーでは、読み込み順序グループは無視されます。

読み込み順序グループの完全な順序付きリストは、 **HKEY_LOCAL_MACHINE \system\currentcontrolset\control**レジストリキーの**ServiceGroupOrder**サブキーの下にあります。

SERVICE_BOOT_START および SERVICE_SYSTEM_START のドライバーには、同じ負荷グループの順序が使用されます。 ただし、すべての SERVICE_BOOT_START ドライバーは、SERVICE_SYSTEM_START ドライバーが読み込まれる前に読み込まれて起動されます。

## <a name="specifying-load-order-group"></a>読み込み順序グループの指定

ドライバーライターは、次のいずれかの方法で、インストール時にドライバーの読み込み順序グループを指定できます。

- ドライバーの INF ファイルの**addservice**ディレクティブによっ*て参照さ*れている、 **loadordergroup**エントリに対して目的の読み込み順序グループを指定する。 この方法については、「ServiceInstall」セクションを参照してください。

- ユーザーモードのインストールプログラムから**CreateService**または**ChangeServiceConfig**を呼び出すときに、 *l*のパラメーターに必要な開始の種類を渡します。 このメソッドについては、Microsoft Windows SDK のドキュメントの**CreateService**と**ChangeServiceConfig**のリファレンスエントリを参照してください。

ドライバーの読み込み順序と読み込み順序のグループの一般的な情報については、「[ドライバーの読み込み順序の指定](https://docs.microsoft.com/windows-hardware/drivers/install/specifying-driver-load-order)」を参照してください。
