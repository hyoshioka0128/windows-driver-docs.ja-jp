---
title: Windows でのブート オプションの概要
description: Windows ブートローダーのアーキテクチャ、ファームウェアに依存しないブート構成、およびブートオプション編集ツールについて説明します。
ms.assetid: 1cc5b1cc-8d0e-4b4e-93fe-272772a3e458
keywords:
- ブートオプション WDK、Windows
- ブートオプションの編集
- マルチブートシステム WDK ブートオプション
- 従来のブートエントリ WDK
- WDK ブート構成データ
- BCD WDK
- BCDEdit ツール
- ブートオプション WDK、編集
- ntldr ツール
- Windows ブートマネージャー WDK
- Bootmgr ツール
- システム固有のブートローダー WDK
- ブートローダー WDK
- ファームウェアに依存しないブートオプション WDK
ms.date: 04/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 25321d11ae8465ec49760b50abfe52d71f291041
ms.sourcegitcommit: d5f54510b9500413dd3084b59cb8869f2f6b13cf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68866765"
---
# <a name="overview-of-boot-options-in-windows"></a>Windows でのブート オプションの概要

Windows ブートローダーアーキテクチャには、ファームウェアに依存しないブート構成と、*ブート構成データ*(BCD) と呼ばれる記憶域システム、およびブートオプション編集ツール (bcdedit) が含まれています。 開発時に、BCDEdit を使用して、Windows 10、Windows 8、Windows Server 2012、Windows 7、および Windows Server 2008 を実行しているコンピューターで、ドライバーのデバッグ、テスト、トラブルシューティングを行うためのブートオプションを構成できます。

> [!CAUTION]
> BCDEdit を使用して BCD を変更するには、管理者特権が必要です。 BCDEdit を使用して一部のブートエントリオプションを変更すると、コンピューターが動作しなくなる可能性があります。 別の方法として、システム構成ユーティリティ (Msconfig.exe) を使用してブート設定を変更することもできます。

## <a name="boot-loading-architecture"></a>ブート読み込みのアーキテクチャ

Windows には、Windows を迅速かつ安全に読み込むように設計されたブートローダーコンポーネントが含まれています。 以前の Windows NT ブートローダーである*ntldr*は、3つのコンポーネントに置き換えられています。

- Windows ブートマネージャー (Bootmgr)

- Windows オペレーティングシステムローダー (Winload .exe)

- Windows resume loader (Winresume .exe)

この構成では、Windows ブートマネージャーは一般的で、各オペレーティングシステムの特定の要件を認識しませんが、システム固有のブートローダーは、読み込むシステムに合わせて最適化されます。

複数のブートエントリを持つコンピューターに Windows の少なくとも1つのエントリが含まれている場合、ルートディレクトリに存在する Windows ブートマネージャーによってシステムが起動され、ユーザーと対話します。 ブートメニューが表示され、選択したシステム固有のブートローダーが読み込まれ、ブートローダーにブートパラメーターが渡されます。

ブートローダーは、各 Windows パーティションのルートディレクトリに存在します。 選択すると、ブートローダーはブートプロセスを引き継ぎ、選択したブートパラメーターに従ってオペレーティングシステムを読み込みます。

## <a name="boot-configuration-data"></a>ブート構成データ

Windows ブートオプションは、BIOS ベースおよび EFI ベースのコンピューターのブート構成データ (BCD) ストアに格納されます。


BCD は、Windows 10、Windows 8、Windows Server 2012、Windows 7、および Windows Server 2008 を実行しているすべてのコンピューターに共通の、ファームウェアに依存しないブートオプションインターフェイスを提供します。 以前のブートオプションのストレージ構成よりも安全性が高くなります。これは、BCD ストアのセキュリティで保護されたロックダウンを許可し、管理者がブートオプションを管理する権限を割り当てることができるためです。 BCD は、実行時およびセットアップのすべての段階で使用できます。 電源状態遷移中に BCD を呼び出し、それを使用して、休止状態後に再開するブートプロセスを定義することもできます。

Bcd ストアが存在するメディア以外のメディアからシステムを起動するときに、BCD をリモートで管理し、BCD を管理できます。 この機能は、デバッグとトラブルシューティングのために非常に重要です。特に、DVD からスタートアップ修復を実行するとき、USB ベースの記憶メディアから、またはリモートから実行しているときに BCD ストアを復元する必要がある場合に役立ちます。

BCD ストアは、使い慣れたオブジェクトと要素のアーキテクチャを備えており、Guid と名前 ("Default" など) を使用して、ブート関連のアプリケーションを正確に識別します。

BCD には、独自のブートオプションセットが含まれています。 これらのブートオプションの詳細については、「 [BCD ブートオプションリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)」を参照してください。

## <a name="editing-boot-options"></a>ブート オプションの編集

Windows でブートオプションを編集するには、Windows に含まれているツールである BCDEdit (BCDEdit) を使用します。 

BCDEdit を使用するには、コンピューターの Administrators グループのメンバーである必要があります。

システム構成ユーティリティ (Msconfig.exe) を使用して、ブート設定を変更することもできます。

Windows でプログラムによってブートオプションを変更するには、Windows Management インストルメント (WMI) インターフェイスを使用してブートオプションを選択します。 この BCD WMI インターフェイスは、ブートオプションをプログラムで変更するのに最適な方法です。 BCD WMI インターフェイスの詳細については、Windows SDK のドキュメントの「[ブート構成データ WMI Provider](https://docs.microsoft.com/previous-versions/windows/desktop/bcd/boot-configuration-data-portal) 」を参照してください。

## <a name="related-topics"></a>関連トピック

- [BCD の編集オプションのリファレンス](bcd-boot-options-reference.md)
- [ブートオプションの編集](editing-boot-options.md)
- [ブートパラメーターの使用](using-boot-parameters.md)

