---
title: アイドル状態の電源管理のスコープ
description: アイドル状態の電源管理のスコープ
ms.assetid: fa34f703-ab02-4a0d-96ae-e7cb89756992
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1eeb6d86aa3675eb1e976303127ea71bc64b753
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606524"
---
# <a name="idle-power-management-scope"></a>アイドル状態の電源管理のスコープ

Storport アイドル電源管理 (IPM) は、アダプターではなく、LUN のアイドル電源管理を提供します。 すべての Lun が低電力状態の場合、Storport IPM はアダプターを低電力状態にしません。 ミニポートドライバーは、アダプターの電源の管理を担当します。

Storport IPM は、次のシステム構成でのみサポートされています。

- 1台の SATA ディスクドライブが取り付けられている SATA アダプターを使用するシステム

Storport IPM は、次のシステム構成ではサポートされていません。

- 直接接続されていないストレージ (FC、iSCSI など) を搭載したシステム

- 外部の記憶域配列と RAID コントローラーを搭載したシステム

- MPIO があるシステム

- SATA 以外のホストバスアダプターを搭載しているシステム

- SATA アダプターに複数のディスクが接続されているシステム
