---
title: IHV 機能拡張の概要
description: IHV 機能拡張の概要
ms.assetid: 446d91e9-3497-4b45-82a6-7f36dd136e08
keywords:
- IHV 拡張 WDK ネイティブ 802.11、IHV 拡張性について
- ネイティブの 802.11 IHV 拡張 WDK、IHV 機能拡張について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65de079b2e210c23b399a77930808326041629c9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537474"
---
# <a name="overview-of-ihv-extensibility"></a>IHV 機能拡張の概要




 

ネイティブの 802.11 フレームワークでは、ネイティブの 802.11 フレームワークの機能を追加する独立系ハードウェア ベンダー (IHV) のサポートを提供します。

たとえば、IHV は、次のいずれかのサポートを提供できます。

-   ポート ベースのネットワーク アクセスのためのアルゴリズムを専用のまたは非標準の認証。 詳細については、[802.11 認証アルゴリズムのサポートの拡張](extending-support-for-802-11-authentication-algorithms.md)を参照してください。

-   データの暗号化の専用のまたは非標準の暗号アルゴリズム。 詳細については、[802.11 の暗号アルゴリズムの拡張サポート](extending-support-for-802-11-cipher-algorithms.md)を参照してください。

-   独自の PHY 構成します。 詳細については、[802.11 PHY 構成のサポートの拡張](extending-support-for-802-11-phy-configurations.md)を参照してください。

ネイティブの 802.11 機能を拡張するには、IHV は、次のコンポーネントを提供する必要があります。

-   拡張可能な局 (ExtSTA) の操作モードをサポートするネイティブ 802.11 ミニポート ドライバー。 このモードの詳細については、[ステーションの操作モードは拡張可能な](extensible-station-operation-mode.md)を参照してください。 ExtSTA 操作モードの方法の詳細については、ネイティブの 802.11 機能を拡張できますを参照してください[802.11 のネイティブ機能を拡張する](extending-native-802-11-functionality.md)します。

-   IHV 拡張 DLL を IHV がサポートする独自の認証アルゴリズムを介して交換されるセキュリティのパケットを処理します。 IHV 拡張機能の DLL を IHV でサポートされているセキュリティ拡張機能に関連するユーザー データの検証だけでなく、これらの認証アルゴリズムの暗号キー派生も担当します。

    IHV 拡張 DLL の詳細については、[802.11 IHV 拡張機能のネイティブの DLL](native-802-11-ihv-extensions-dll4.md)を参照してください。

-   IHV ユーザー インターフェイス (UI) 拡張 DLL を接続および検証され、IHV 拡張機能の DLL によって処理されるセキュリティ設定を構成する 802.11 のネイティブ ユーザー インターフェイスを拡張するものです。

    IHV UI 拡張機能の DLL の詳細については、[ネイティブ 802.11 IHV UI 拡張機能の DLL](native-802-11-ihv-ui-extensions-dll2.md)を参照してください。

IHV によって提供されるモジュールの詳細については、[ネイティブ 802.11 ソフトウェア アーキテクチャ](native-802-11-software-architecture.md)を参照してください。

セキュリティで保護された実行環境を提供するには、IHV が、以下を実行します。

1.  イベントで、暗号化キーなど、機密情報を記録したり、デバッグ ログしないでください。

2.  使用[CryptProtectMemory](https://go.microsoft.com/fwlink/p/?linkid=64677) 、メモリに格納されている機密性の高い暗号化キーを保護および[SecureZeroMemory](https://go.microsoft.com/fwlink/p/?linkid=64678)キーを使用して完了時にメモリをオフにします。

3.  IHV 拡張機能の特定の部分を扱う、[ネットワーク プロファイル](configuration-through-a-network-profile.md)として信頼されていないデータが攻撃者によって操作されていることがあります。 プロファイルの IHV 拡張機能の一部は、802.11 自動構成モジュール (ACM) およびメディア固有モジュール (MSM) に対して非透過的は検証されません。 (を参照してください[ネイティブ 802.11 ソフトウェア アーキテクチャ](native-802-11-software-architecture.md)これらのモジュールと構成の管理パスの説明についてはします)。この IHV 拡張機能のデータは、すべてのバッファー オーバーフローまたは特権のローカルの昇格を引き起こす可能性のある攻撃を防ぐため適切に解析する必要があります。

 

 





