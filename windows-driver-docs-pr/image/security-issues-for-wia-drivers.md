---
title: WIA ドライバーに関するセキュリティの問題
description: WIA ドライバーに関するセキュリティの問題
ms.assetid: 5d8fc015-cbf5-43a3-8f65-3ebb17754417
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7869102247ce3d88a400666d2657d2458eeb0c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531667"
---
# <a name="security-issues-for-wia-drivers"></a>WIA ドライバーに関するセキュリティの問題





サービスの実行、 **LocalSystem**アカウントは、危険であることができますので**LocalSystem**は基本的には管理者であり、したがって、コンピューターのほぼすべてのリソースへのアクセスがあります。 設計上の欠陥やバグのあるコードで実行されているサービスで**LocalSystem**破壊的なユーザーの特権の昇格可能性があります。 Windows XP には 2 つの新しい組み込みのサービス アカウントが導入された**LocalService**と**NetworkService**サービスのセキュリティ侵害の影響を軽減するために特別に設計されました。 これら 2 つの新しいアカウントは、「サービスとしてログイン」を除く、任意の特別な権限のない制限付きユーザー アカウントです。

このセキュリティ イニシアチブ合わせて WIA サービスが実行される、 **LocalService** Microsoft Windows Server 2003 以降のオペレーティング システムのバージョンでのアカウント。

Windows Server 2003 では、前に、WIA サービスと WIA ドライバーが下で実行される場合を想定して開発された**LocalSystem**します。 これは、Windows Server 2003 を使用して変更し、ドライバー開発者が意識する必要があるいくつかの影響がします。 このセクションには、WIA ドライバー開発者が発生する可能性があります、一般的な問題の一覧が含まれています。 問題を解決する方法を含むです。

このドキュメントに記載されているプラクティスに従うにより、Windows XP、Windows Server 2003、またはそれ以降のオペレーティング システム バージョンで実行されているかどうかを開発、WIA ドライバーが正しく機能します。

[WIA セキュリティ上の一般的な問題](common-wia-security-problems.md)

[WIA セキュリティのベスト プラクティス](wia-security-best-practices.md)

デバイス ドライバーのセキュリティの詳細については、次を参照してください。、[デバイス オブジェクトのセキュリティで保護する](https://msdn.microsoft.com/library/windows/hardware/ff563688)と[セキュリティで保護されたデバイスのインストールを作成する](https://msdn.microsoft.com/library/windows/hardware/ff540212)セクション。

 

 




