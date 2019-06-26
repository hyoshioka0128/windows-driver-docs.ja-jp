---
title: INF Reboot ディレクティブ
description: 再起動のディレクティブは、呼び出し元がインストールが完了したら、システムの再起動を通知することを示します。
ms.assetid: 0E2640EA-921D-4677-82EF-EF9707254E66
keywords:
- INF 再起動ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF Reboot Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2ad3ad61e5b4bcf5b610a29d01de988ded3b071
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370037"
---
# <a name="inf-reboot-directive"></a>INF Reboot ディレクティブ

A**再起動**ディレクティブでは、呼び出し元がインストールが完了したら、システムの再起動を通知することを示します。

```ini
[DDInstall]
  
Reboot
```

**警告**  、**再起動**ディレクティブが処理されるで直接指定した場合のみ、 **\[DDInstall\]** セクション。

 

**再起動**システムを再起動する必要が自動的に検出されるため、デバイスの一部として検出される共通の条件に基づく Windows にインストール用の INF ファイルでディレクティブが指定されてほとんどないです。インストールします。 たとえば、システムは呼び出し元に通知ファイルのコピー操作のいくつかターゲット ファイルが使用する場合、またはデバイスは、インストール時に自動的に再開できない場合、再起動が必要です。 **再起動**ディレクティブは、いくつかのシステムの再起動は、システム自体によって自動的に検出できないドライバーのインストール後は必要では常に特定の条件がある場合にのみ使用する必要があります。

再起動のディレクティブを指定すると、システムの再起動がこの INF インストール セクションを使用して任意のデバイスのインストールを完了する必要があることが呼び出し元に通知されます。 ときに、インストールが開始された関数を通じてなど[ **UpdateDriverForPlugAndPlayDevices**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)、 [ **DiInstallDriver** ](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)、または[ **DiInstallDevice**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldevice)、その結果、 *NeedReboot* out パラメーターを TRUE に設定されているこれらのルーチンの。

<a name="remarks"></a>注釈
-------

Windows 7 以降でのドライバーを使用してデバイスのインストールで、**再起動**ディレクティブは、システムの再起動がインストールの完了に必要なことを通知する、呼び出し元で常に得られます。

Windows 8 以降では、上記で説明した動作は、1 つの場合にのみ発生します。 または、複数のデバイスをインストールするのには既に開始されています。 新しいドライバーのインストール中に、デバイスを再起動するのではなく、システムは、システムの再起動が、新しいドライバーのインストールを完了するために必要であるを呼び出し元に通知します。 インストールするデバイスが現在開始されていない場合、システムは、システムの再起動を必要とせずに、インストールを実行しようとします。 再起動も必要がありますのインストールの操作のいずれかが必要な場合に注意してください。 たとえば、コピーするいくつかのファイルの変換先ファイルの場所は、現在使用中に場合、このシステムの再起動はインストールを完了する必要も。

 

 





