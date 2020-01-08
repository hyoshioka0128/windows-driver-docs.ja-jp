---
title: Storport i/o モデルの概要
description: Storport i/o モデルの概要
ms.assetid: 9220b01e-725f-4a03-87f1-402c0686cccd
keywords:
- Storport ドライバー WDK、i/o
- I/o WDK Storport
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ee4cd96f3c8d5e294ab1e1f261b4ddcbccc9dec
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606430"
---
# <a name="storport-io-model-overview"></a>Storport i/o モデルの概要

このセクションでは、Storport ドライバーの i/o モデルについて説明し、このモデルを SCSI ポートドライバーのものと比較します。 Storport i/o モデルは、高速バスおよび記憶装置のパフォーマンスを最大限に活用できるように設計されたいくつかの機能で構成されています。

Storport ドライバーは、i/o のプッシュモデルを使用します。 これは、ドライバーが i/o 要求をミニポートドライバーに非同期で転送することを意味します。これは、ミニポートドライバーが入力を要求するのを待たずに、重複するパケットの最大数になります。 プッシュモデルでは、ポートドライバーは i/o 要求のフローを制御し、要求をミニポートドライバーにプッシュします。

一方、SCSI ポートドライバーは、i/o のプルモデルを使用します。 I/o のプルモデルでは、SCSI ポートドライバーはミニポートドライバーに i/o 要求を同期的に転送し、次の i/o 要求を送信する前にミニポートドライバーが新しい入力を要求するまで待機します。 さらに、ミニポートドライバーは、i/o 要求のフローを制御し、ポートドライバーから要求を取得します。

SCSI ポートドライバーの i/o モデルの詳細については、「 [Scsi ポート I/o モデル](scsi-port-i-o-model.md)」を参照してください。
