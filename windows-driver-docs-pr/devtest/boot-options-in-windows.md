---
title: Windows でのブート オプションの概要
description: Windows ブート ローダーのアーキテクチャ、ファームウェアに依存しないブート構成、および編集ツールのブート オプションについて説明します。
ms.assetid: 1cc5b1cc-8d0e-4b4e-93fe-272772a3e458
keywords:
- ブート オプション WDK、Windows
- ブート オプションの編集
- マルチブート システム WDK ブート オプション
- WDK の従来のブート エントリ
- ブート構成データ WDK
- BCD の WDK
- BCDEdit ツール
- ブート オプション、WDK の編集
- ntldr ツール
- Windows ブート マネージャーの WDK
- Bootmgr ツール
- システムに固有のブート ローダー WDK
- ブート ローダー WDK
- WDK のファームウェアに依存しないブート オプション
ms.date: 04/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: b55951890633b00a988af2aa2f7047071436d964
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371656"
---
# <a name="overview-of-boot-options-in-windows"></a>Windows でのブート オプションの概要

Windows ブート ローダーのアーキテクチャにはと呼ばれるファームウェアに依存しないブート構成と記憶域システムが含まれています*ブート構成データ*(BCD) およびブート オプションを編集ツールの BCDEdit (BCDEdit.exe)。 開発中は、デバッグ、テスト、および Windows 10、Windows 8、Windows Server 2012、Windows 7、および Windows Server 2008 を実行しているコンピューターでのドライバーのトラブルシューティングのブート オプションを構成するのに BCDEdit を使用できます。

> [!CAUTION]
> BCDEdit を使用して BCD を変更するには、管理者特権が必要です。 BCDEdit を使用していくつかのブート エントリ オプションを変更すると、コンピューターをしなくなる可能性があります。 代わりに、システム構成ユーティリティ (MSConfig.exe) を使用して、ブート設定を変更します。

## <a name="boot-loading-architecture"></a>ブート アーキテクチャの読み込み

Windows には、迅速かつ安全に Windows を読み込むように設計されたブート ローダー コンポーネントが含まれています。 前の Windows NT ブート ローダー *ntldr*、3 つのコンポーネントが置き換えられます。

- Windows ブート マネージャー (Bootmgr.exe)

- Windows オペレーティング システム ローダー (Winload.exe)

- Windows ローダー (Winresume.exe) を再開します。

この構成で、Windows ブート マネージャーはジェネリックと各オペレーティング システムの特定の要件に関係なくシステムに固有のブートローダーが読み込まれるシステム用に最適化されたときにします。

ブート エントリを複数使用しているコンピューターには、Windows の少なくとも 1 つのエントリが含まれているルート ディレクトリにある Windows ブート マネージャーはシステムが起動し、ユーザーと対話します。 ブート メニューが表示されます、読み込み、選択したシステムに固有のブート ローダーおよびブート ローダーにブート パラメーターを渡します。

ブート ローダーは、Windows の各パーティションのルート ディレクトリに存在します。 選択すると、ブート ローダーはブート プロセスを実行し、選択したブート パラメーターに従ってオペレーティング システムを読み込みます。

## <a name="boot-configuration-data"></a>ブート構成データ

Windows のブート オプションが格納されている BIOS および EFI ベースのコンピューター上のブート構成データ (BCD) ストアにします。


BCD は、Windows 10、Windows 8、Windows Server 2012、Windows 7、および Windows Server 2008 を実行しているすべてのコンピューターの共通のファームウェアに依存しないブート オプションのインターフェイスを提供します。 により、BCD ストアのセキュリティで保護されたロックダウンをにより、管理者はブート オプションを管理するための権限を割り当てるため、以前のブート オプション ストレージ構成よりも方が安全です。 BCD は、実行時に、セットアップのすべてのフェーズ中に使用できます。 でも、電源の状態遷移中に BCD を呼び出すし、休止状態の後に再開するにブート プロセスの定義に使用できます。

BCD をリモートで管理でき、システムの BCD ストアが存在するメディア以外のメディアからブートするときに BCD を管理することができます。 この機能は、デバッグとトラブルシューティングは、特にと BCD ストアを復元して、DVD からスタートアップ修復の実行中に非常に重要な USB ベースの記憶域メディア、またはリモートからでもです。

BCD ストアで、使い慣れたそのオブジェクトから要素のアーキテクチャは Guid と"Default"などの名前ブートに関連するアプリケーションを正確に識別するためにします。

BCD には、独自のブート オプション セットが含まれています。 これらの詳細については、ブート オプションを参照してください[BCD のブート オプションの参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

## <a name="editing-boot-options"></a>ブート オプションの編集

Windows でのブート オプションを編集するには、BCDEdit (BCDEdit.exe)、Windows に含まれるツールを使用します。 

BCDEdit を使用するには、コンピューターの Administrators グループのメンバーがあります。

ブート設定を変更するのにシステム構成ユーティリティ (MSConfig.exe) を使用することもできます。

プログラムで Windows のブート オプションを変更するには、ブート オプションを Windows Management インストルメント (WMI) インターフェイスを使用します。 BCD WMI インターフェイスは、ブート オプションをプログラムで変更する最適な方法です。 BCD WMI インターフェイスについては、次を参照してください。[ブート構成データの WMI プロバイダー](https://docs.microsoft.com/previous-versions/windows/desktop/bcd/boot-configuration-data-portal) Windows SDK のドキュメント。

## <a name="related-topics"></a>関連トピック

- [Bcdedit オプション リファレンス](bcd-boot-options-reference.md)
- [ブート オプションの編集](editing-boot-options.md)
- [ブート パラメーターを使用します。](using-boot-parameters.md)
- [ブート構成データ](https://go.microsoft.com/fwlink/p/?linkid=74322)

