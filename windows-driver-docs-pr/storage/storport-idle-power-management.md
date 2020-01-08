---
title: Storport アイドル状態の電源管理の概要
description: Storport アイドル状態の電源管理の概要
ms.assetid: 1ad47775-4d7a-47c4-83eb-774e58c863d3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 100d38c7aa33ee41cb292b819ee1eb645eadb4f5
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606379"
---
# <a name="storport-idle-power-management-overview"></a>Storport アイドル状態の電源管理の概要

Storport アイドル状態の電源管理 (IPM) を使用すると、classpnp および disk class ドライバーは、一定期間アイドル状態になったときに SCSI 停止ユニットコマンドをディスクデバイスに送信できます。 アイドル期間は、システム管理者が構成できます。 Storport ミニポートドライバーは、Storport ミニポートドライバーがコマンドを使用して電力を節約する方法を担います。 以下のセクションでは、IPM の詳細について説明します。

- [Scope](ipm-scope.md)

- [予想](ipm-assumptions.md)

- [構成と使用方法](ipm-configuration-and-usage.md)

- [ハードディスクドライブのアイドルタイムアウト](ipm-hard-disk-drive-idle-timeout.md)
