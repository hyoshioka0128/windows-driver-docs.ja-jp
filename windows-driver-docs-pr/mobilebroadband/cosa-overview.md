---
title: COSA の概要
description: COSA の概要
ms.assetid: 45D69B8D-69C1-488B-AC52-D8DEB337F878
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9dc4c16fd217ced9ab881a20ac388b189a50101f
ms.sourcegitcommit: 257850d61aa5d1db707dc2f30721319b650e47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73801172"
---
# <a name="cosa-overview"></a>COSA の概要

COSA (国とオペレーターの設定資産) は、モバイルブロードバンド用に Windows デバイスをプロビジョニングするために、携帯電話会社 (MOs) が Windows 10 バージョン1703以降で使用する新しい形式です。 Windows 8、Windows 8.1、および1703より前の Windows 10 のバージョンの既存の APN データベース (apndatabase .xml) は、新しいプロビジョニングフレームワークによって ingestible される COSA に変換されました。 以前のバージョンの Windows では、デスクトップデバイスのプロビジョニングに古い APN データベースが引き続き使用されていることに注意してください。

古い APN データベースの詳細については、「 [apn データベースの概要](apn-database-overview.md)」を参照してください。

Desktop COSA で MOs に構成できる使用可能な設定の一覧については、「[デスクトップ cosa/APN データベースの設定](desktop-cosa-apn-database-settings.md)」を参照してください。

## <a name="faq"></a>FAQ

- [MOs が COSA で指定できる設定は何ですか。](#settings)
- [新しい MO 設定の適用をトリガーするイベントは何ですか。](#events)
- [モデムから使用される SIM 情報はどのようなものですか。](#SIMinfo)
- [APN を最適なものにするためのアルゴリズムはありますか。](#APNmatch)
- [COSA データベースはどこに格納され、apndatabase .xml のように視覚的に検査することができますか。](#location)
- [デバイスが Windows 10 バージョン 1607 (またはそれ以前) から Windows 10 バージョン1703に更新されるとどうなりますか。カスタムまたは手動で作成した APNs は移行されますか?データベースの既定値よりも優先されますか。](#update)
- [**従量制課金接続**設定が**オフ**から**オン**に変わる場合があるのはなぜですか。](#metered)

### <a href="" id="settings"></a>MOs が COSA で指定できる設定は何ですか。

設定は、apndatabase で構成されているものとほとんど同じですが、いくつかの例外と新しい追加機能があります。 詳細については、「 [Planning your desktop COSA/APN データベースの送信](planning-your-desktop-cosa-apn-database-submission.md)」の表を参照してください。

### <a href="" id="events"></a>新しい MO 設定の適用をトリガーするイベントは何ですか。

Windows プロビジョニングエンジンは、次の3つのイベントによって設定の変更を検索します。 

1.  物理 SIM の挿入または削除 (ICCID での変更)
2.  ESIM の再構成 (ICCID での変更)
3.  デバイスが起動したとき

### <a href="" id="SIMinfo"></a>モデムから使用される SIM 情報はどのようなものですか。

MO/MVNO 検出の場合、Windows はモデムの SIM の SPN を使用して、COSA データベースで使用可能なプロファイルに最適な照合を試みます。

### <a href="" id="APNmatch"></a>APN を最適なものにするためのアルゴリズムはありますか。

Windows 10 バージョン1703より前のバージョンの Windows では、MOs は自動接続の順序を指定できます。 Windows 10、バージョン1703以降では、使用可能なすべての APNs でラウンドロビン方式が引き続き使用されますが、アルゴリズムで使用される特定の順序はなくなります。

### <a href="" id="location"></a>COSA データベースはどこに格納され、apndatabase .xml のように視覚的に検査することができますか。

COSA は、Windows 10 のプロビジョニングパッケージ (ppkg) の形式です。 これは Windows\Provisioning\COSA\Microsoft フォルダーにあります。 7 Zip ファイルマネージャー ([www.7-Zip.org](https://go.microsoft.com/fwlink/p/?linkid=844795)) などのサードパーティ製ツールを使用して、コンテンツを視覚的に調べることができます。

デバイスイメージに指定されている場合、COSA の OEM 拡張機能は、COSA\ oem フォルダーにあることに注意してください。 詳細については、「[国とオペレーターの設定資産をカスタマイズする](https://docs.microsoft.com/windows-hardware/customize/desktop/customize-cosa)」を参照してください。

### <a href="" id="update"></a>デバイスが Windows 10 バージョン1607以前から Windows 10 バージョン1703以降に更新された場合はどうなりますか。 カスタムまたは手動で作成した APNs は移行されますか? データベースの既定値よりも優先されますか。

アップグレード後に、COSA によって apndatabase .xml が置き換えられます。 APN が以前のバージョンでプロビジョニングされている場合は、カスタム、手動、またはデバイスがデータベースを通じてプロビジョニングされているかどうかに関係なく、バージョン1703へのアップグレードの一環として移行され、デバイスは引き続き接続に使用します。追加の操作は必要ありません。 手動でプロビジョニングされた APNs は、バージョン1607以前と同様に、データベースの既定値よりも優先されます。

### <a href="" id="metered"></a>従量制課金接続として設定する 設定が **オフ** から**オン** に変わることがあるのはなぜですか。

Windows オペレーティングシステムの更新プログラムには、COSA データベースの更新プログラムが含まれる場合があります。 データベースが更新されると、プロビジョニングエンジンによって携帯電話プロファイルが削除される場合があります。 データベースの更新がインストールされた後にシステムを再起動すると、プロビジョニングエンジンによって携帯電話プロファイルが再インストールされます。 この操作では、ユーザー設定を既定値にリセットします。 たとえば、**従量制課金接続**の変更を**Off**から**On**に設定します。 この動作は仕様です。
