---
title: APN データベースの概要
description: APN データベースの概要
ms.assetid: 699b797e-c225-47ba-96a5-26b15c91a759
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70450eca7688c90045326ca12bd76c04309204d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560349"
---
# <a name="apn-database-overview"></a>APN データベースの概要

APN データベース、または apndatabase.xml は、自社のネットワークにモバイル ブロード バンド エクスペリエンスを構成する Mobile 演算子 (MOs) を使用するプロビジョニング データベースです。 Windows 8、Windows 8.1、および Windows 10、Windows 10 バージョン 1703 より前に、のバージョンで使用可能になります。

APN データベースは Windows 10 バージョン 1703 以降 COSA と呼ばれる新しい形式に置換されます。 Windows 8、Windows 8.1、およびバージョンの Windows 10 バージョン 1703 を引き続き Windows 10 は APN データベースを使用する前に、バージョン 1703 以降は COSA を使用します。 

COSA に関する詳細については、次を参照してください。 [COSA 概要](cosa-overview.md)します。

MOs が APN データベースで構成できる使用可能な設定の一覧を表示するには、次を参照してください。[デスクトップ COSA/APN データベースの設定](desktop-cosa-apn-database-settings.md)します。

## <a name="span-idapndbconspanspan-idapndbconspanapn-database-contents"></a><span id="apndbcon"></span><span id="APNDBCON"></span>APN データベースの内容


モバイル ブロード バンド ネットワークに接続する場合、ユーザーは、通常、次の情報を提供します。

- Global System for Mobile Communications (GSM) ネットワークなど、APN で**data.contoso.com**します。

- CDMA ネットワークで特別なを含むアクセス文字列ダイヤル コードなど **\#777**、やなどのネットワーク アクセスの識別子 (NAI)  <strong>ann@contoso.com</strong>します。

- ユーザーの資格情報 (ユーザー名とパスワード) のネットワーク接続。

具体的には、APN データベースには、次のデータが含まれています。

-   **演算子の id データ**

    -   GSM ネットワークでの International Mobile IMSI (Subscriber Identity) またはネットワークで使用する統合型回線カード識別子 (ICCID) 範囲データベース エントリを送信できます。 モバイルの仮想ネットワークの演算子 (MVNO) 場合は、IMSIs またはサブスクライバーの id のモジュールからモバイル ネットワーク オペレーター (MNO) リースされた (SIM) ICC Id の 1 つまたは複数の範囲を指定できます。

    -   CDMA ネットワークでは、各プロバイダーの ID、またはプロバイダーの名前の新しいデータベースのエントリを送信できます。

    -   MVNOs を識別する方法を理解を参照してください。 [MVNOs のエクスペリエンスを提供する](delivering-experiences-for-mvnos.md)します。

-   **APNs の購入の一覧とアクセス文字列**

    -   GSM ネットワークでは、ユーザー名とサブスクリプションの購入のパスワードを持つ APNs の一覧。

    -   CDMA ネットワークでは、サブスクリプションの購入に NAIs の一覧。

-   **インターネットの一覧は、APNs に接続し、文字列にアクセス**

    -   GSM ネットワークでは、ユーザー名と、インターネットに接続するためのパスワードを持つ APNs の一覧。

    -   CDMA ネットワークでは、インターネットへの接続に使用される NAIs の一覧。

-   **アカウント URL のエクスペリエンス**web サイトを初めて購入アカウントの URL が発生します。

-   **証明書のデータ**証明書のメタデータをプロビジョニングするアカウントの情報。 これにより、証明書の発行者名とサブジェクト名が含まれていて、アカウント プロビジョニングを購入して web サイトにはユーザーの提供されている web サービスの承認されていることを確認するために使用します。

APN データベースの XML スキーマの詳細については、次を参照してください。 [APN データベースのスキーマ リファレンス](apn-database-schema-reference.md)します。

## <a name="span-idabndbsubspanspan-idabndbsubspanapn-database-submission-and-maintenance"></a><span id="abndbsub"></span><span id="ABNDBSUB"></span>APN データベースの送信とメンテナンス


新しい APN 要求または既存の 1 つは、参照を更新する場合[COSA/APN データベース送信](cosa-apn-database-submission.md)します。
 





