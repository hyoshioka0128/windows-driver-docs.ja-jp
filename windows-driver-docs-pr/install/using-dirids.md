---
title: Dirids の使用
description: Dirids の使用
ms.assetid: 231bc313-b5c3-48ef-b2e2-c4e287517679
keywords:
- dirids WDK
- INF ファイル WDK デバイス インストールでは、ディレクトリの識別子
- WDK の INF ファイルのディレクトリ識別子
- WDK の INF ファイルのディレクトリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef026ea881e2e5a2f130c8b99832cd9a1df69bdb
ms.sourcegitcommit: cab03f9f6b1143a29be74a894e917b26762a42ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2019
ms.locfileid: "65852351"
---
# <a name="using-dirids"></a>Dirids の使用





INF ファイルに表示されるディレクトリの多くは、ディレクトリの識別子を使用して表すことができます (*dirids*)、特定のディレクトリを識別する番号であります。 アプリケーションは、使用できますが、関連付けられているシステム定義のディレクトリに再割り当てできません*dirids*の値は-1 ~ 32767 です。

作成する*dirids* 65534、あるいは 65536 というと使用を 32768 からユーザー定義の値を持つ、 **SetupSetDirectoryId**関数 (Microsoft Windows SDK のドキュメントで説明)。

注意してくださいを*dirid* 65535 の値を持つと見なされますと同義、 *dirid* -1 という値が、後者 (*dirid* -1) をお勧めします。

使用する場合*dirids* INF ファイルでは、次の 2 つのガイドラインを検討してください。

1. INF ファイルのエントリの構文が明示的に指定します、 *dirid*値 (、 [ **INF DestinationDirs セクション**](inf-destinationdirs-section.md)など)、その値を数値として表現します。

   次の例では、この構文を示しています。

   ```cpp
   [DestinationDirs]
   DefaultDestDir = 11  ;  \system32 directory on Windows 2000 and later versions
   ```

2. INF ファイルのエントリの構文は、ファイルのパスを指定する場合は、このパスの一部またはすべてを表す、システム指定文字列を置換を使用できます。 この置換では、次の形式があります。

   **%**<em>Dirid</em>**%**

   このフォームは、パーセント (%) で構成されています文字の後に、 *dirid*を指定するディレクトリの後にもう 1 つのパーセント (%)文字。 終端の円記号 (\)文字は、次のファイル名またはパスに追加のディレクトリからこの式を区切ります<strong>します。</strong>

   次の例では、この構文を示しています。

   ```cpp
   [aic78xx_Service_Inst]
   ServiceBinary = %12%\aic78xx.sys
   ```

   完全に展開すると、前の例に示すように、パスは次のようになります*c:*\\*windows*\\*system32* \\ *。ドライバー*\\*aic78xx.sys* (で Windows がインストールされていると仮定すると、 *c:*\\*windows*ディレクトリ)。 注意してくださいを文字列の置換、または %*dirid*の例外に、文字列が想定される場所 % のフォームで使用できます、 [ **INF 文字列セクション**](inf-strings-section.md)の INF ファイル。

   次の 2 つの例の表示文字列の置換がどのように*いない*使用します。

   ```cpp
   [DestinationDirs]
   DefaultDestDir = %11%  ; Error! - number expected

   [aic78xx_Service_Inst]
   ServiceBinary = 12\aic78xx.sys  ; Error! - unknown directory name
   ```

   最初の例の構文で、 **DefaultDestDir**エントリの数値にするには、その値が必要です。 ただし、% 11% の式を文字列に展開します。 2 番目の例では、INF ライターようするためのものの値を設定、 **ServiceBinary**ドライバー (詳細については、次の表を参照してください) が含まれているディレクトリ内のファイルに入力します。 Windows がコンピューターでおそらく存在しない「12」をという名前のディレクトリ内の指定のファイルを探し、エラーが発生します。

次の表は一般的に使用されるいくつか*dirids*とディレクトリを表します。 最もよくデバイス INF ファイルおよびドライバーの INF ファイルで指定された値は、テーブルの上部に表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">宛先ディレクトリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>01</strong></p></td>
<td align="left"><p><em>SourceDrive</em><strong>: \</strong><em>pathname</em> (INF ファイルのインストール元のディレクトリ)</p></td>
</tr>
<tr class="even">
<td align="left"><p>"<strong>10</strong>"</p></td>
<td align="left"><p>Windows ディレクトリ。</p>
<p>これに相当<em>%systemroot%</em>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>11</strong></p></td>
<td align="left"><p>システム ディレクトリ。</p>
<p>これに相当<em>%systemroot%</em><strong>\</strong><em>system32</em> Windows 2000 と Windows の以降のバージョン.</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>12</strong></p></td>
<td align="left"><p>ドライバーのディレクトリ。</p>
<p>これに相当<em>%systemroot%</em><strong>\</strong><em>system32</em><strong>\</strong><em>ドライバー</em> Windows 2000 と Windows の以降のバージョン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>13</strong></p></td>
<td align="left"><p>ドライバー パッケージの<a href="https://msdn.microsoft.com/windows/hardware/drivers/install/driver-store">ドライバー ストア</a>ディレクトリ。</p>
<p>Windows 8.1 と Windows の以降のバージョンでは、ドライバー パッケージがインポートされたドライバー ストア ディレクトリへのパスを指定します。

使用しない<a href="inf-delfiles-directive.md" data-raw-source="[DelFiles](inf-delfiles-directive.md)">DelFiles</a>対象のファイルで<strong>DestinationDirs</strong>が含まれています<em>dirid</em> 13。

省略可能なサブディレクトリ内にある、 <strong>SourceDiskFiles</strong>セクション ファイルは、サブディレクトリ内にあると一致する必要があります、 <strong>DestinationDirs</strong>セクションのこのファイルに適用されるエントリ。

使用しない<a href="inf-copyfiles-directive.md" data-raw-source="[CopyFiles](inf-copyfiles-directive.md)">CopyFiles</a>対象のファイルの名前を変更する<strong>DestinationDirs</strong>が含まれています<em>dirid</em> 13。
</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>17</strong></p></td>
<td align="left"><p>INF ファイル ディレクトリ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>18</strong></p></td>
<td align="left"><p>ディレクトリをヘルプします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>20</strong></p></td>
<td align="left"><p>フォント ディレクトリ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>21</strong></p></td>
<td align="left"><p>ビューアーのディレクトリ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>23</strong></p></td>
<td align="left"><p>色のディレクトリ (ICM) (<em>いない</em>プリンター ドライバーをインストールするために使用)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>24</strong></p></td>
<td align="left"><p>システム ディスクのルート ディレクトリ。</p>
<p>これは、Windows のファイルがインストールされているディスクのルート ディレクトリです。 たとえば場合、 <em>dirid</em> 10 は"<em>C:\winnt</em>"、し<em>dirid</em> 24 は、"<em>C:\</em>"。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>25</strong></p></td>
<td align="left"><p>共有ディレクトリ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>30</strong></p></td>
<td align="left"><p>「円弧システム パーティション」とも呼ばれる、ブート ディスクのルート ディレクトリ。 (これがかによって表されると同じディレクトリにあります<em>dirid</em> 24)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>50</strong></p></td>
<td align="left"><p>システム ディレクトリ</p>
<p>これに相当<em>%systemroot%</em><strong>\</strong><em>システム</em>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>51</strong></p></td>
<td align="left"><p>スプール ディレクトリ (<em>いない</em>−「プリンター ドライバー インストールに使用される<a href="https://msdn.microsoft.com/library/windows/hardware/ff560821">プリンター Dirids</a>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>52</strong></p></td>
<td align="left"><p>ドライバーのスプール ディレクトリ (<em>いない</em>プリンター ドライバーをインストールするために使用)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>53</strong></p></td>
<td align="left"><p>ユーザー プロファイル ディレクトリ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>54</strong></p></td>
<td align="left"><p>ディレクトリで<em>Ntldr.exe</em>と<em>Osloader.exe</em>が配置されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>55</strong></p></td>
<td align="left"><p>プリント プロセッサ ディレクトリ (<em>いない</em>プリンター ドライバーをインストールするために使用)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-1</strong></p></td>
<td align="left"><p>絶対パス</p></td>
</tr>
</tbody>
</table>

 

*Dirid* 16384 32767 までの値は特別なシェル フォルダーの予約されています。 次の表は*dirid*これらのフォルダーの値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">シェルの特別なフォルダー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>16406</strong></p></td>
<td align="left"><p><em>すべてのします メニュー</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16407</strong></p></td>
<td align="left"><p><em>すべてのします menu \programs</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>16408</strong></p></td>
<td align="left"><p><em>すべてのします \programs\startup</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16409</strong></p></td>
<td align="left"><p><em>すべての \desktop</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>16415</strong></p></td>
<td align="left"><p><em>すべての Users\Favorites</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16419</strong></p></td>
<td align="left"><p><em>すべてのバックアップ データ</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>16422</strong></p></td>
<td align="left"><p><em>プログラム ファイル</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16425</strong></p></td>
<td align="left"><p><em>%SystemRoot%\SysWOW64</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>16426</strong></p></td>
<td align="left"><p><em>%ProgramFiles(x86)%</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16427</strong></p></td>
<td align="left"><p><em>Program Files\Common</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>16428</strong></p></td>
<td align="left"><p><em>%ProgramFiles(x86)%\Common</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16429</strong></p></td>
<td align="left"><p><em>すべての Users\Templates</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>16430</strong></p></td>
<td align="left"><p><em>すべての Users\Documents</em></p></td>
</tr>
</tbody>
</table>

 

このテーブルで定義されている値だけでなく*Setupapi.h*、CSIDL_ のいずれかを使用することができます*Xxx*で定義されている値*Shlobj.h*します。 定義する、 *dirid*この表に記載いないフォルダーの値を CSIDL_ を 16384 (0x4000) を追加*Xxx*値。 CSIDL_ の詳細については*Xxx*値が、Windows SDK のマニュアルを参照してください。

 

 





