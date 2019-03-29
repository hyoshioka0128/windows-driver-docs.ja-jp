---
title: ネットワーク プロファイルの概要
description: ネットワーク プロファイルの概要
ms.assetid: b7d902db-4918-4e9f-a7e0-3bb6c5ed1dfb
keywords:
- ネットワーク プロファイル ネイティブ 802.11 IHV の WDK 拡張 DLL、ネットワーク プロファイルについて
- XML フラグメントを WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 999a7f743f3ee842b649840420c3caec99a97d04
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580398"
---
# <a name="network-profile-overview"></a>ネットワーク プロファイルの概要




 

ネットワーク プロファイルは、基本的なサービスのセット (BSS) ネットワークに接続の属性を定義します。 ネットワーク プロファイルは、データの XML フラグメントで構成されます。 Windows vista の場合は、ネットワーク プロファイルには、次の XML フラグメントが含まれています。

<a href="" id="profile-name--required-"></a>**プロファイルの名前 (必須)**  
サービスであるネットワーク プロファイルの名前は、BSS ネットワークの識別子 (SSID) を設定します。

<a href="" id="standard-802-11-connectivity-settings--required-"></a>**(必須) 802.11 の標準の接続設定**  
この XML フラグメントは、BSS ネットワークの種類 (インフラストラクチャまたは独立) またはワイヤレス LAN (WLAN) のセキュリティの種類など、ネットワーク接続の 802.11 の標準の設定で構成されます。 オペレーティング システムでは、標準的な接続設定を処理し、それらにワイヤレス WLAN アダプターを構成します。

<a href="" id="ihv-connectivity-extensions--optional-"></a>**IHV 接続の拡張機能が (省略可能)**  
この XML フラグメントは、拡張機能を IHV で定義されているネットワーク接続で構成されます。 オペレーティング システムは、処理の IHV 拡張機能の DLL に、接続の拡張機能に渡します。 DLL が WLAN アダプター専用の拡張機能の構成を担当します。

<a href="" id="standard-802-11-security-settings--optional-"></a>**標準な 802.11 セキュリティの設定 (省略可能)**  
この XML フラグメントから成る標準 802.11、BSS に使用する認証と暗号アルゴリズムの種類などの認証および暗号の設定はネットワーク接続。 オペレーティング システムでは、標準的なセキュリティ設定を処理し、それらに WLAN アダプターを構成します。

<a href="" id="ihv-security-extensions--optional-"></a>**IHV セキュリティ拡張機能 (省略可能)**  
この XML フラグメントは、ネットワーク セキュリティ、IHV で定義されている拡張機能で構成されます。 IHV 拡張機能には、次のいずれかを指定できます。

-   標準的なセキュリティ設定。

    IHV 拡張機能の DLL によって管理されている、WLAN アダプターの DLL は、堅牢なセキュリティ ネットワークの関連付けなど、セキュリティ アルゴリズム責任を負います ( [RSNA](https://docs.microsoft.com/windows-hardware/drivers/network/rsna-overview)) 認証アルゴリズムまたは[AES CCMP](https://docs.microsoft.com/windows-hardware/drivers/network/aes-ccmp)暗号アルゴリズム。 オペレーティング システムの責任がなくなります。 このような状況で IHV 拡張機能の DLL のアルゴリズムを処理するか WLAN アダプターに処理をオフロードする独自のメソッドを提供します。

-   独自のセキュリティ設定。

    IHV 拡張機能の DLL は、標準または専有アルゴリズムなど、オペレーティング システムでサポートされていないセキュリティ アルゴリズムのサポートを提供できます。 DLL は、アルゴリズムの処理を担当するまたは WLAN アダプターに処理をオフロードする独自のメソッドを提供します。

ネイティブの 802.11 XML スキーマの詳細については、Microsoft Windows SDK のマニュアルを参照してください。

 

 





