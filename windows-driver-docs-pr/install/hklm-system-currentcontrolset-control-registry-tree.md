---
title: HKLM\SYSTEM\CurrentControlSet\Control レジストリ ツリー
description: HKLM\SYSTEM\CurrentControlSet\Control レジストリツリーには、システムの起動およびデバイス構成のいくつかの側面を制御するための情報が含まれています。
ms.assetid: 58eacd32-425d-4224-8d37-21e2caf124cf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff80b48420cf93804e9d7d1d3c345c4badbb2eb5
ms.sourcegitcommit: e480dcfea893ef6c85b2dfb5827f51b740466262
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71278374"
---
# <a name="hklmsystemcurrentcontrolsetcontrol-registry-tree"></a>HKLM\\システム\\CurrentControlSet\\Control レジストリツリー





**HKLM\\system\\CurrentControlSetControlレジストリツリーには、システムの起動およびデバイス構成のいくつかの側面を制御するための情報が含まれています。\\** 特に重要なサブキーは次のとおりです。

<a href="" id="class"></a>**講義**  
システム上の[デバイスセットアップクラス](device-setup-classes.md)に関する情報が含まれています。 セットアップクラスの GUID を使用して名前が付けられた各クラスのサブキーがあります。 各サブキーには、クラスインストーラー (存在する場合)、登録されたクラスの上位フィルタードライバー、登録済みクラスの下位フィルタードライバーなどのセットアップクラスに関する情報が含まれています。

<a href="" id="codeviceinstallers"></a>**CoDeviceInstallers**  
システムに登録されているクラス固有の共同インストーラーに関する情報を格納します。

<a href="" id="deviceclasses"></a>**DeviceClasses 場合**  
システム上のデバイスインターフェイスに関する情報を格納します。 各[デバイスインターフェイスクラス](device-interface-classes.md)にサブキーがあります。

 

 





