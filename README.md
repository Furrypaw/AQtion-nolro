Fork of Aquantia's AQtion linux driver with LRO disabled and patched to work on Proxmox hosts
===========
This fork is specifically intended for our institute's Proxmox cluster, but may be of use for others as well.

Why?
-----------
As can be read in the original README.txt for this driver, Large Receive Offload (LRO) is enabled by default, but does
not play nice with IP forwarding, routing, or bridging, which is exactly what we need our cluster's exit nodes to do.
Indeed, the version of atlantic built into the kernel, which also has LRO enabled, has caused those nodes to lose
connection and crash frequently.  Compiling the driver and disabling the feature fixed this for us.  Also, the install
scripts provided with the driver do not support Proxmox out of the box.  This fork fixes both of these issues for our
installation, and may do so for yours, too.

How?
-----------
We have modified the install scripts to work on Proxmox VE host systems and turned off LRO permanently in 'aq_cfg.h'.
Functionally, everything (installing and using) should remain the same as documented in the original distribution.

What else?
-----------
If you use dkms to auto-install the driver, you will find that it fails because of dkms's version check. (The in-tree
atlantic driver follows the kernel's versioning, while this one has its own, resulting in it looking older to dkms.)
To fix this, you can force disable the version checking by creating the file
'/usr/share/dkms/modules_to_force_install/atlantic' (create the directory as well if necessary) with content
<code>
atlantic
</code>

Below you can find the original unmodified readme.

AQUANTIA AQtion (atlantic) linux driver
===========
This is a latest development preview of aquantia's atlantic linux kernel driver for AQtion family of multigigabit adapters.
Please read technical details in [README.txt](https://github.com/Aquantia/AQtion/blob/master/README.txt)

Notice this is an **experimental software**. For stable driver version please either visit http://www.aquantia.com or take the driver
bundled with your linux kernel.

Being experimental, it has the following agreement and limitations:

AQUANTIA SOFTWARE LICENSE AGREEMENT – EXPERIMENTAL USE SOFTWARE
===========

The terms of this Aquantia Software License Agreement (“Agreement”) govern and control your use of the Aquantia software and associated materials (collectively, “Software”) available for download at this site. 

IMPORTANT - READ BEFORE COPYING, INSTALLING OR USING.
----------------------------------

Do not copy, install, or use this Software until you, on behalf of the company, partnership or business entity that you represent (“You”) have carefully read the following terms and conditions. 
By copying, installing, or otherwise using the Software, You agree to be bound by the terms of this Agreement. If You do not agree to the terms of this Agreement, do not copy, install, or use the Software. 

EXPERIMENTAL NATURE OF THE SOFTWARE; DISCLAIMER OF WARRANTIES
----------------------------------

YOU ACKNOWLEDGE AND UNDERSTAND THAT YOU ARE RECEIVING A VERSION OF THE SOFTWARE THAT IS IN AN UNTESTED, EXPERIMENTAL FORM AND MAY CONTAIN SIGNIFICANT ERRORS, OMISSIONS, AND PROBLEMS.  THE SOFTWARE IS PROVID¬ED "AS IS."  AQUANTIA DIS¬CLAIMS ALL WAR-RAN¬TIES OF ANY KIND, EXPRESS OR IMPLIED, IN¬CLUDING, BUT NOT LIMITED TO, WAR¬RAN¬TIES OF PERFOR¬MANCE OR MER¬CHANTABILI¬TY OR FITNESS FOR A PARTICU¬LAR PURPOSE OR WARRANTY AGAINST INFRINGEMENT. 
YOU BEAR ALL RISK RELAT¬ING TO USE OF THE SOFTWARE AND THE QUALITY AND PERFORMANCE OF THE SOFTWARE.  Aquantia does not warrant that the Soft¬ware will meet your require¬ments, operate without interruption or be error free.  Aquantia further does not warrant or assume responsibility for the accuracy or completeness of any information, text, graphics, links, or other items contained within the Software.

LICENSE
----------------------------------

Subject to all of the terms and conditions of this Agreement, Aquantia grants to You a non-exclusive, non-assignable, copyrighted license to use the Software for evaluation purposes only.  As part of such use, You may copy the Software onto a single computer for your personal use, and You may make one back-up copy of the Software, provided that You retain all proprietary rights notices included in the original version.

LICENSE RESTRICTIONS
----------------------------------

You may NOT: (i) use or copy the Software except as provided in this Agreement; (ii) rent or lease the Software to any third party; (iii) assign this Agreement or transfer the Software without the express written consent of Aquantia; (iv) modify, adapt, or translate the Software in whole or in part except as provided in this Agreement; (v) reverse engineer, decompile, or disassemble the Software; (vi) attempt to modify or tamper with the normal function of a license manager that regulates usage of the Software; (vii) distribute, sublicense or transfer any components of the Software.  **PRODUCTION USE OF THE SOFTWARE IS NOT PERMITTED**.

NO OTHER RIGHTS
===========

No rights or licenses are granted by Aquantia to You, expressly or by implication, with respect to any proprietary information or patent, copyright, mask work, trademark, trade secret, or other intellectual property right owned or controlled by Aquantia, except for the limited, evaluation license to the Software as expressly provided in this Agreement.

OWNERSHIP OF SOFTWARE AND COPYRIGHTS
----------------------------------
The Software is licensed, not sold. Title to all copies of the Software remains with Aquantia. The Software is copyrighted and protected by the laws of the United States and other countries and international treaty provisions. You may not remove any copyright notices from the Software. You agree to prevent any unauthorized copying of the Software. Aquantia may make changes to the Software, or to items referenced therein, at any time without notice, but is not obligated to support or update the Software.

FEEDBACK
----------------------------------

You agree that Aquantia may, at its sole discretion, use any and all feedback you provide, including without limitation, any flaws, errors, bugs, anomalies, problems, suggestions for improvement or other modifications and any other feedback with respect to the Software (collectively, “Feedback”) without any payment of royalties or other liabilities or obligations.  You represent, warrant and covenant that you have the right to provide Feedback to Aquantia.

LIMITATION OF LIABILITY
----------------------------------

IN NO EVENT SHALL AQUANTIA OR ITS SUPPLIERS BE LIABLE FOR ANY DAMAGES OF ANY KIND WHATSOEVER, WHETHER DIRECT, INCIDENTIAL, CONSEQUENTIAL, PUNITIVE OR OTHERWISE (INCLUDING, WITHOUT LIMITATION, LOST PROFITS, BUSINESS INTERRUPTION, OR LOST INFORMATION) ARISING OUT OF THE USE OF OR INABILITY TO USE THE SOFTWARE, EVEN IF AQUANTIA HAS BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGES. SOME JURISDICTIONS PROHIBIT EXCLUSION OR LIMITATION OF LIABILITY FOR IMPLIED WARRANTIES OR CONSEQUENTIAL OR INCIDENTAL DAMAGES, SO THE ABOVE LIMITATION MAY NOT APPLY TO YOU. YOU MAY ALSO HAVE OTHER LEGAL RIGHTS THAT VARY FROM JURISDICTION TO JURISDICTION.  In the event that the above exclusion does not apply, You agree that Aquantia’s entire liability for any and all claims of any kind whatsoever in connection with the Software or this Agreement shall be limited to $100.

TERMINATION OF THIS AGREEMENT
----------------------------------

Aquantia may terminate this Agreement at any time if You violate its terms. Upon termination, You will immediately destroy the Software or return all copies of the Software to Aquantia.

APPLICABLE LAWS
----------------------------------

Claims arising under this Agreement shall be governed by the laws of the State of California, without regard to principles of conflict of laws. You agree that the terms of the United Nations Convention on Contracts for the International Sale of Goods does not apply to this Agreement. You may not export the Software in violation of applicable export laws and regulations. Aquantia is not obligated under any other agreements unless they are in writing and signed by an authorized representative of Aquantia.
