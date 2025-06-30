
<!-- <hr>

  You can also find my articles on my <a href="https://scholar.google.com/citations?user=1B_T56IAAAAJ" target="_blank">Google Scholar profile</a>.

<hr> -->

<heading><strong>Back on Track: Bundle Adjustment for Dynamic Scene Reconstruction</strong> </heading>
  <table width="100%" align="center" border="0" cellspacing="0" cellpadding="20">  
    <tr onmouseout="batrack_stop()" onmouseover="batrack_start()">  
            <td width="40%">
              <div class="one">
                <div class="two" id='batrack_shape' style="display: flex; justify-content: center; height: 100%; width: 100%;">
                  <video autoplay muted loop playsinline style="height: 100%;">
                    <source src="https://wrchen530.github.io/projects/batrack/static/videos/davis_3.mp4" type="video/mp4">
                    Your browser does not support the video tag.
                  </video>
                </div>
                <img src='https://wrchen530.github.io/images/batrack.png' style="width: 100%;" id='batrack_img'/>
              </div>       
              <script type="text/javascript">
              function batrack_start() { 
              document.getElementById('batrack_img').style.opacity = "0";
              document.getElementById('batrack_shape').style.opacity = "1";
              }
              function batrack_stop() { 
              document.getElementById('batrack_shape').style.opacity = "0"; 
              document.getElementById('batrack_img').style.opacity = "1";
              }
              batrack_stop()
              </script>
            </td>
      <td valign="top" width="75%">
            <papertitle>
            <strong>
            <a href="https://wrchen530.github.io/projects/batrack" target="_blank">Back on Track: Bundle Adjustment for Dynamic Scene Reconstruction</a>
            </strong>
            </papertitle>
      <br>
          <a href="https://wrchen530.github.io/" target="_blank">Weirong Chen</a>, 
          <strong>Ganlin Zhang</strong>, 
          <a href="https://fwmb.github.io/" target="_blank">Felix Wimbauer</a>, 
          <a href="https://rui2016.github.io/" target="_blank">Rui Wang</a>, 
          <a href="https://arnike.github.io/" target="_blank">Nikita Araslanov</a>, 
          <a href="https://www.robots.ox.ac.uk/~vedaldi/" target="_blank">Andrea Vedaldi</a>, 
          <a href="https://cvg.cit.tum.de/members/cremers" target="_blank">Daniel Cremers</a>
        <br>
          <em><strong>ICCV</strong>, 2025</em>
        <br>
        <a href="https://wrchen530.github.io/projects/batrack/" target="_blank">Github Repo (Coming Soon) </a> | 
        <a href="https://arxiv.org/abs/2504.14516" target="_blank">ArXiv</a> | 
        <a href="https://wrchen530.github.io/projects/batrack/" target="_blank">Project website</a>
        <br>
        A method for consistent dynamic scene reconstruction via motion decoupling, bundle adjustment, and global refinement.
         </td>
    </tr>
  </table>
  <hr>



  <heading><strong>Splat-SLAM: Globally Optimized RGB-only SLAM with 3D Gaussians</strong> </heading>
  <table width="100%" align="center" border="0" cellspacing="0" cellpadding="20">  
      <td width="40%">
        <div class="one">
        <img src="/images/publications/splatslam.jpg" width="100%"> </div>
      </td>
      <td valign="top" width="75%">
            <papertitle>
            <strong>
              <a href="https://openaccess.thecvf.com/content/CVPR2025W/VOCVALC/papers/Sandstrom_Splat-SLAM_Globally_Optimized_RGB-only_SLAM_with_3D_Gaussians_CVPRW_2025_paper.pdf" target="_blank">Splat-SLAM: Globally Optimized RGB-only SLAM with 3D Gaussians</a>
            </strong>
            </papertitle>
      <br>
          <a href="https://eriksandstroem.github.io/" target="_blank">Erik Sandström*</a>, 
          <strong>Ganlin Zhang*</strong>, 
          <a href="https://scholar.google.com/citations?user=ml3laqEAAAAJ" target="_blank"> Keisuke Tateno</a>, 
          <a href="https://moechsle.github.io/" target="_blank"> Michael Oechsle</a>, 
          <a href="https://youmi-zym.github.io/" target="_blank"> Youmin Zhang</a>, 
          <a href="https://manthan99.github.io/" target="_blank"> Manthan Patel</a>, 
          <a href="https://vision.ee.ethz.ch/people-details.OTAyMzM=.TGlzdC8zMjg3LC0xOTcxNDY1MTc4.html" target="_blank"> Luc Van Gool</a>, 
          <a href="https://oswaldm.github.io/" target="_blank"> Martin R. Oswald</a>, 
          <a href="https://federicotombari.github.io/" target="_blank"> Federico Tombari</a>
        <br>
          <em><strong>CVPRW</strong>, 2025</em>
        <br>
        <a href="https://github.com/google-research/Splat-SLAM" target="_blank">Github Repo</a> | 
        <a href="https://openaccess.thecvf.com/content/CVPR2025W/VOCVALC/papers/Sandstrom_Splat-SLAM_Globally_Optimized_RGB-only_SLAM_with_3D_Gaussians_CVPRW_2025_paper.pdf" target="_blank">Paper</a> | 
        <a href="https://openaccess.thecvf.com/content/CVPR2025W/VOCVALC/supplemental/Sandstrom_Splat-SLAM_Globally_Optimized_CVPRW_2025_supplemental.pdf" target="_blank">Supp</a>
        <br>
        We use a keyframe based frame to frame tracker based on dense optical flow connected to a pose graph for global consistency. For dense mapping, we resort to a 3DGS representation, suitable for extracting both dense geometry and rendering from.
      </td>
  </table>
  <hr>

  
  <heading><strong>GlORIE-SLAM: Globally Optimized RGB-only Implicit Encoding Point Cloud SLAM</strong> </heading>
  <table width="100%" align="center" border="0" cellspacing="0" cellpadding="20">  
    <tr onmouseout="glorie_stop()" onmouseover="glorie_start()">  
            <td width="40%">
              <div class="one">
                <div class="two" id='glorie_shape'>
                  <video  autoplay muted loop playsinline width="100%">
                    <source src="/images/publications/glorie.mp4" type="video/mp4">
                        Your browser does not support the video tag.
                    </video>
                </div>
                <img src='/images/publications/glorie.jpg' style="width: 100%;"/>
              </div>        
              <script type="text/javascript">
              function glorie_start() { 
              document.getElementById('glorie_shape').style.opacity = "1";
              }
              function glorie_stop() { 
              document.getElementById('glorie_shape').style.opacity = "0"; 
              }
              glorie_stop()
              </script>
            </td>
      <td valign="top" width="75%">
            <papertitle>
            <strong>
            <a href="https://zhangganlin.github.io/GlORIE-SLAM/index.html" target="_blank">GlORIE-SLAM: Globally Optimized RGB-only Implicit Encoding Point Cloud SLAM</a>
            </strong>
            </papertitle>
      <br>
          <strong>Ganlin Zhang*</strong>, 
          <a href="https://eriksandstroem.github.io/" target="_blank">Erik Sandström*</a>, 
          <a href="https://youmi-zym.github.io/" target="_blank"> Youmin Zhang</a>, 
          <a href="https://manthan99.github.io/" target="_blank"> Manthan Patel</a>, 
          <a href="https://vision.ee.ethz.ch/people-details.OTAyMzM=.TGlzdC8zMjg3LC0xOTcxNDY1MTc4.html" target="_blank"> Luc Van Gool</a>, 
          <a href="https://oswaldm.github.io/" target="_blank"> Martin R. Oswald</a>
        <br>
          <em>Preprint on ArXiv, 2024</em>
        <br>
        <a href="https://github.com/zhangganlin/GlORIE-SLAM" target="_blank">Github Repo </a> | 
        <a href="https://arxiv.org/abs/2403.19549" target="_blank">ArXiv</a> | 
        <a href="https://zhangganlin.github.io/GlORIE-SLAM/index.html" target="_blank">Project website</a>
        <br>
        1. A monocular SLAM pipeline with deformalbe neural pointcloud scene representation. <br>
        2. Novel DSPO layer for BA, which can jointly optimize depth map, depth scale and camera pose. <br>
         </td>
    </tr>
  </table>
  <hr>



<heading><strong>Revisiting Rotation Averaging: Uncertainties and Robust Losses</strong> </heading>
<table width="100%" align="center" border="0" cellspacing="0" cellpadding="20">  
    <td width="40%">
      <div class="one">
      <img src="/images/publications/rotationAverage.png" width="100%"> </div>
    </td>
    <td valign="top" width="75%">
          <papertitle>
          <strong>
            <a href="https://openaccess.thecvf.com/content/CVPR2023/papers/Zhang_Revisiting_Rotation_Averaging_Uncertainties_and_Robust_Losses_CVPR_2023_paper.pdf" target="_blank">Revisiting Rotation Averaging: Uncertainties and Robust Losses</a>
          </strong>
          </papertitle>
    <br>
        <strong>Ganlin Zhang</strong>,
        <a href="https://vlarsson.github.io/" target="_blank">Viktor Larsson</a>,
        <a href="https://cvg.ethz.ch/team/Dr-Daniel-Bela-Barath" target="_blank">Daniel Barath</a>
      <br>
        <em><strong>CVPR</strong>, 2023</em>
      <br>
      <a href="https://github.com/zhangganlin/GlobalSfMpy" target="_blank">Github Repo</a> | 
      <a href="https://arxiv.org/abs/2303.05195" target="_blank">ArXiv</a>
      <br>
      1. Better model the underlying noise distributions by directly propagating the uncertainty from the point correspondences into the rotation averaging. <br>
      2. Integrate a variant of the MAGSAC++ loss into the rotation averaging, instead of using the classical robust losses.
    </td>
</table>
<hr>

