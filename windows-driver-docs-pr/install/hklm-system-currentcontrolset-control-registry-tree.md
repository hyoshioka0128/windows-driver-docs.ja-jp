---
title: Hklm \system\currentcontrolset\control レジストリ ツリー
description: Hklm \system\currentcontrolset\control レジストリ ツリーには、システムの起動を制御する情報とデバイスの構成の一部の側面が含まれています。
ms.assetid: 58eacd32-425d-4224-8d37-21e2caf124cf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28e40e0717c39243aec0df5c6e4b1ae7bc0efd97
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549397"
---
# <a name="hklmsystemcurrentcontrolsetcontrol-registry-tree"></a>HKLM\\システム\\CurrentControlSet\\レジストリ ツリーのコントロール





**HKLM\\システム\\CurrentControlSet\\コントロール**レジストリ ツリーには、システムの起動とデバイスの構成の一部の側面を制御するための情報が含まれています。 次のサブキーは、特に重要なのです。

<a href="" id="class"></a>**クラス**  
に関する情報を含む、[デバイス セットアップ クラス](device-setup-classes.md)システムにします。 各クラスのセットアップ クラス GUID を使用してという名前のサブキーがあります。 各サブキーには、情報が含まれています。 セットアップ クラスの場合は、クラスなどインストーラー (存在する場合)、クラス上フィルター ドライバーでは、登録されていると低いフィルター ドライバーのクラスを登録します。

クラスの各サブキーと呼ばれるその他のサブキーが含まれています。*ソフトウェア キー* (または、*ドライバー キー*) システムにインストールされているそのクラスの各デバイス インスタンス。 デバイス インスタンス ID、底が 10、4 桁の序数値を使用して、各ソフトウェア キーと呼びます。

<a href="" id="codeviceinstallers"></a>**CoDeviceInstallers**  
システムに登録されているクラスに固有の共同インストーラーについて説明します。

<a href="" id="deviceclasses"></a>**DeviceClasses**  
システム上のデバイス インターフェイスに関する情報が含まれています。 各サブキーがある[デバイス インターフェイス クラス](device-interface-classes.md)とデバイスのインターフェイス クラスに登録されているインターフェイスのインスタンスごとにこれらのサブキーの下のエントリ。

 

 





