---
title: COSA の概要
description: COSA の概要
ms.assetid: 45D69B8D-69C1-488B-AC52-D8DEB337F878
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e852750541d155843bbd6651a53974301f70f191
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572034"
---
# <a name="cosa-overview"></a>COSA の概要

COSA、または国と演算子の設定の資産は、Windows 10 バージョン 1703 ではモバイル ブロード バンドの Windows デバイスをプロビジョニングするには、後で Mobile 演算子 (MOs) を使用して、新しい形式です。 Windows 8、Windows 8.1、および 1703 する前に Windows 10 のバージョンからの既存の APN データベース (apndatabase.xml) は、これは、新しいプロビジョニング フレームワークによって ingestible COSA に変換がされました。 この以前のバージョンの Windows デスクトップ デバイスをプロビジョニングするため、古い APN データベースを使用し続けることに注意してください。

以前の APN データベースの詳細については、次を参照してください。 [APN データベースの概要](apn-database-overview.md)します。

デスクトップ COSA で構成できます MOs の使用可能な設定の一覧を表示するには、次を参照してください。[デスクトップ COSA/APN データベースの設定](desktop-cosa-apn-database-settings.md)します。

## <a name="faq"></a>FAQ

- [MOs が COSA で指定できる設定とは](#settings)
- [どのようなイベントは、新しい月の設定の適用をトリガーしますか。](#events)
- [COSA はモデムから SIM 情報を使用しますか。](#SIMinfo)
- [適切な APN 対応するためのアルゴリズムではありますか。](#APNmatch)
- [COSA データベースが格納されている、およびその視覚的に検査できる apndatabase.xml のような場合でしょうか。](#location)
- [デバイスが Windows 10 バージョン 1607 (またはそれ以前) から Windows 10 バージョン 1703 を更新すると起こりますか。カスタムまたは手動で作成した APNs は移行されますか。まだが優先度、データベースからの既定値をでしょうか。](#update)

### <a href="" id="settings"></a> MOs が COSA で指定できる設定とは

設定は、apndatabase.xml、いくつかの例外と新しい追加機能で構成されているどのような MOs と同じではそれほど変わりません。 詳細については、内のテーブルを参照してください。[計画デスクトップ COSA/APN データベース提出](planning-your-desktop-cosa-apn-database-submission.md)します。

### <a href="" id="events"></a> どのようなイベントは、新しい月の設定の適用をトリガーしますか。

3 つのイベントはトリガーの設定の変更を検索する Windows のプロビジョニング エンジンです。 

1.  挿入または物理 SIM (ICCID の変更) の削除
2.  (ICCID の変更)、eSIM の再構成
3.  デバイスが起動する場合

### <a href="" id="SIMinfo"></a> COSA はモデムから SIM 情報を使用しますか。

月/MVNO 検出では、Windows は、SIM から SPN を使用して、モデムで COSA データベースに、使用可能なプロファイルに最適なものを作成しようとします。

### <a href="" id="APNmatch"></a> 適切な APN 対応するためのアルゴリズムではありますか。

Windows 10 バージョン 1703 では、前に Windows のバージョンで MOs はワン順序を指定できます。 すべての利用可能な APNs によるラウンド ロビン方式を使用する Windows 10 バージョン 1703 以降を続行しますが、アルゴリズムを使用して、特定の順序はありません。

### <a href="" id="location"></a> COSA データベースが格納されている、およびその視覚的に検査できる apndatabase.xml のような場合でしょうか。

COSA は Windows 10 のプロビジョニング パッケージ (.ppkg) の形式です。 Windows\Provisioning\COSA\Microsoft フォルダーになります。 7 Zip ファイル マネージャーなどのサード パーティ製ツールを使用することができます ([www.7-Zip.org](https://go.microsoft.com/fwlink/p/?linkid=844795))、視覚的にその内容を検査します。

注意 COSA、OEM の拡張機能、デバイスのイメージで指定されている場合 COSA\OEM フォルダーにします。 詳細については、次を参照してください。[国と演算子の設定の資産をカスタマイズ](https://msdn.microsoft.com/windows/hardware/commercialize/customize/desktop/customize-cosa)します。

### <a href="" id="update"></a> Windows 10 バージョン 1607 または Windows 10 バージョン 1703 以降に以前から、デバイスを更新すると起こりますか。 カスタムまたは手動で作成した APNs は移行されますか。 まだが優先度、データベースからの既定値をでしょうか。

COSA では、アップグレード後に apndatabase.xml が置き換えられます。 カスタム、manual、またはデータベースを使用してデバイス プロビジョニングするかどうか、以前のバージョンで、APN が準備され、バージョン 1703 へのアップグレードの一部として移行し、デバイスは引き続き、接続の追加アクションを必要とせずに使用します。 プロビジョニングは手動で APNs も優先順位を持つデータベースからの既定値を前をバージョン 1607 でだけです。

