---
layout: archive
title: "Selected Projects"
permalink: /projects/
author_profile: true
# header:
#   og_image: "research/ecdf.png"
---

<!-- <nbsp> -->

<!-- {% include base_path %}

{% assign ordered_pages = site.projects | sort:"order_number" %}

{% for post in ordered_pages %}
  {% include archive-single.html type="grid" %}
{% endfor %} -->


<html>
  <head>
  <meta name="google-site-verification" content="xDNWUvx6Q5EWK5YYSyKvK8DZTmvXhKsGX203Ll-BFFE" >	
  <meta name="generator" content="HTML Tidy for Linux/x86 (vers 11 February 2007), see www.w3.org">
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
  <style type="text/css">
  @import url(https://fonts.googleapis.com/css?family=Roboto:400,400italic,500,500italic,700,700italic,900,900italic,300italic,300);
  /* @import url(https://fonts.googleapis.com/css?family=Roboto:300,400,500,700|Roboto+Slab:100,300,400,500,700|Material+Icons); */
    /* Color scheme stolen from Sergey Karayev */
    .one
    {
    position: relative;
    }
    .two
    {
    position: absolute;
    transition: opacity .2s ease-in-out;
    -moz-transition: opacity .2s ease-in-out;
    -webkit-transition: opacity .2s ease-in-out;
    }
    .fade {
     transition: opacity .2s ease-in-out;
     -moz-transition: opacity .2s ease-in-out;
     -webkit-transition: opacity .2s ease-in-out;
    }
    span.highlight {
        background-color: #ffffd0;
    }
  </style>




<hr>
  <heading><strong>Holo-Spot: Accessible Robot Control in Mixed Reality</strong> </heading>
  <table width="100%" align="center" border="0" cellspacing="0" cellpadding="20">  
    <tr onmouseout="holo_stop()" onmouseover="holo_start()">  
            <td width="40%">
              <div class="one">
                <div class="two" id='holo_shape'>
                  <!-- <img src='/images/projects/holospot.gif' width="100%"> -->
                  <video  width="100%" muted autoplay loop>
                    <source src="/images/projects/holospot.mp4" type="video/mp4">
                        Your browser does not support the video tag.
                    </video>
                  </div>
                  <img src='/images/projects/holospot.png' width="100%"/>
                </div>
                            
              <script type="text/javascript">
              function holo_start() { 
              document.getElementById('holo_shape').style.opacity = "1";
              }
              function holo_stop() { 
              document.getElementById('holo_shape').style.opacity = "0"; 
              }
              holo_stop()
              </script>
            </td>
      <td valign="top" width="75%">
            <papertitle>
            <strong>
            <a href="https://zhangganlin.github.io/Holo-Spot-Page/index.html" target="_blank">Holo-Spot: Accessible Robot Control in Mixed Reality</a>
            </strong>
            </papertitle>
      <br>
          <strong>Ganlin Zhang*</strong>,
          <a href="https://dehezhang2.github.io/" target="_blank">Deheng Zhang*</a>,
          <a href="https://github.com/DecAd3" target="_blank"> Longteng Duan*</a>,
          <a href="https://github.com/guo-han" target="_blank"> Guo Han*</a>
        <br>
          <em>Course project of Mixed Realiy 2022 in ETH Zurich</em>
        <br>
        <a href="https://dehezhang2.github.io//holo-spot" target="_blank">Github Repo </a> | 
        <a href="https://zhangganlin.github.io/Holo-Spot-Page/index.html" target="_blank">Project website</a>
        <br>
        In this project, we design, implement and deploy a mixed-reality-based method with HoloLens 2 that enables users to control the Boston Dynamics Spot robot.</td>
    </tr>
  </table>
  <hr>


<heading><strong>NICE-SLAM with Adaptive Feature Grids</strong> </heading>
<table width="100%" align="center" border="0" cellspacing="0" cellpadding="20">
  <tr onmouseout="nice_stop()" onmouseover="nice_start()"> 
    
    <td width="40%">
      <div class="one">
      <div class="two" id = 'nice_shape'>
        <img src="/images/projects/niceslam.gif" width="100%" > </div>
      <img src='/images/projects/niceslam.png' width="100%" >
      </div>
      
      <script type="text/javascript">
      function nice_start() { 
      document.getElementById('nice_shape').style.opacity = "1";
      }
      function nice_stop() { 
      document.getElementById('nice_shape').style.opacity = "0"; 
      }
      nice_stop()
      </script>
    </td>

    <td valign="top" width="75%">
          <papertitle>
          <strong>
            NICE-SLAM with Adaptive Feature Grids
          </strong>
          </papertitle>
    <br>
        <strong>Ganlin Zhang</strong>,
        <a href="https://dehezhang2.github.io/"  target="_blank">Deheng Zhang</a>,
        <a href="https://www.linkedin.com/in/feichi-lu-171840094/" target="_blank"> Feichi Lu</a>,
        <a href="https://www.linkedin.com/in/anqi-li-244547130/" target="_blank"> Anqi Li</a>
      <br>
        <em>Course project of 3D Vision 2022 in ETH Zurich</em>
      <br>
      <a href="https://github.com/zhangganlin/NICE-SLAM-with-Adaptive-Feature-Grids" target="_blank">Github Repo</a>
      <br>
      In this project, we present a sparse version of NICE-SLAM, which is a SLAM system incorporating the idea of Voxel Hashing into <a href="https://pengsongyou.github.io/nice-slam"> NICE-SLAM</a> framework. Instead of initializing feature grids in the whole space, voxel features near the surface are adaptively added and optimized.
    </td>
  </tr>
</table>
<hr>

<heading><strong>Optimization by Particle Swarm Using Surrogates via Bunch-Kaufman Pivoting and Standard Optimization</strong> </heading>
<table width="100%" align="center" border="0" cellspacing="0" cellpadding="20">  
    <td width="40%">
      <div class="one">
      <center><img src="/images/projects/opus.png" width="80%"> </center></div>
    </td>
    <td valign="top" width="75%">
          <papertitle>
          <strong>
            Optimization by Particle Swarm Using Surrogates via Bunch-Kaufman Pivoting and Standard Optimization
          </strong>
          </papertitle>
    <br>
        <strong>Ganlin Zhang*</strong>,
        <a href="https://dehezhang2.github.io/" target="_blank">Deheng Zhang*</a>,
        <a href="https://www.linkedin.com/in/junpeng-gao-04574917b/" target="_blank"> Junpeng Gao*</a>,
        <a href="https://www.linkedin.com/in/yu-hong-b06322178/" target="_blank"> Yu Hong*</a>
      <br>
        <em>Course project of Advanced System Lab 2022 in ETH Zurich</em>
      <br>
      <a href="https://github.com/zhangganlin/OPUS-via-Bunch-Kaufman-pivoting-and-standard-optimization" target="_blank">Github Repo</a>
      <br>
      Focus on speeding up black-box optimization algorithm OPUS from paper <a href="https://acl.inf.ethz.ch/teaching/fastcode/2022/project/project-ideas/particle-swarm.pdf" target="_blank">Particle Swarm with Radial Basis Function Surrogates for Expensive Black-box Optimization</a> by Rommel G. Regis. 
      <br>
      Besides, we implement the speed-up C++ version of Bunch-Kaufman Pivoting.
    </td>
</table>
<hr>

<heading><strong>Improved PSMNet for Deep Stereo Disparity Estimation</strong> </heading>
<table width="100%" align="center" border="0" cellspacing="0" cellpadding="20">  
    <td width="40%">
      <div class="one">
      <img src="/images/projects/psm.png" width="100%"> </div>
    </td>
    <td valign="top" width="75%">
          <papertitle>
          <strong>
            Improved PSMNet for Deep Stereo Disparity Estimation
          </strong>
          </papertitle>
    <br>
        <strong>Ganlin Zhang*</strong>,
        <a href="https://github.com/hkkkpang" target="_blank">Haokai Pang*</a>,
        <a href="https://github.com/ucabxs0" target="_blank"> Xinyu Shen*</a>,
        <a href="https://github.com/yunyingzhu" target="_blank"> Yunying Zhu*</a>
      <br>
        <em>Course project of Deep Learning 2021 in ETH Zurich</em>
      <br>
      <a href="https://github.com/zhangganlin/Improved-PSMNet-for-Deep-Stereo-Disparity-Estimation" target="_blank">Github Repo</a>
      <br>
      Combining PSM Net, group-wise corr, dilatedResNet, semantic segmentation information to estimate accurate disparity of stereo image pairs efficiently.
    </td>
</table>
<hr>

<heading><strong>Robot Art: Using Robot Arm to Draw Pictures</strong> </heading>
<table width="100%" align="center" border="0" cellspacing="0" cellpadding="20">  
  <tr onmouseout="roboart_stop()" onmouseover="roboart_start()">  
          <td width="40%">
            <div class="one">
            <div class="two" id = 'roboart_shape'>
              <video  width="100%" muted autoplay loop>
                <source src="/images/projects/roboart.mp4" type="video/mp4">
                    Your browser does not support the video tag.
                </video>
              </div>
            <img src='/images/projects/roboart.png' width="100%">
            </div>
            
            <script type="text/javascript">
            function roboart_start() { 
            document.getElementById('roboart_shape').style.opacity = "1";
            }
            function roboart_stop() { 
            document.getElementById('roboart_shape').style.opacity = "0"; 
            }
            roboart_stop()
            </script>
          </td>
    <td valign="top" width="75%">
          <papertitle>
          <strong>
          <a href="https://sites.google.com/berkeley.edu/ee106a-roboart" target="_blank">Robot Art: Using Robot Arm to Draw Pictures</a>
          </strong>
          </papertitle>
    <br>
        <strong>Ganlin Zhang*</strong>,
        <a href="https://www.linkedin.com/in/teng-xu-%E8%AE%B8-%E8%85%BE-243812180/" target="_blank">Teng Xu*</a>,
        <a href="https://weijielyu.github.io/" target="_blank"> Weijie Lyu*</a>,
        <a href="https://toytag.net/" target="_blank"> Zhenzhong Tang*</a>
        <a href="https://www.linkedin.com/in/ziyuanhu/" target="_blank"> Ziyuan Hu*</a>
      <br>
        <em>Course project of Introduction to Robotics 2019 in UC Berkeley</em>
      <br>
      <a href="https://github.com/Ten1o/EE106A-RoboArt" target="_blank">Github Repo</a> | 
      <a href="https://sites.google.com/berkeley.edu/ee106a-roboart" target="_blank">Project website</a>
      <br>
      We design a path-finding algorithm that could generate a path to draw a potrait/character in one stroke. Then we use our self-designed control system to draw these path. This project would be useful for any arm-robots with at least 4 joints.
    </td>
  </tr>
</table>
<hr>

