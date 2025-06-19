<!DOCTYPE html>
<html>
<head>
  <meta http-equiv="Content-type" content="text/html;charset=utf-8">
  <link rel="stylesheet" type="text/css" href="/demos/latest/css/gollum.css" media="all">
  <link rel="stylesheet" type="text/css" href="/demos/latest/css/editor.css" media="all">
  <link rel="stylesheet" type="text/css" href="/demos/latest/css/dialog.css" media="all">
  <link rel="stylesheet" type="text/css" href="/demos/latest/css/template.css" media="all">
  
  

  <!--[if IE 7]>
  <link rel="stylesheet" type="text/css" href="/demos/latest/css/ie7.css" media="all">
  <![endif]-->

  <script type="text/javascript">
      var baseUrl = '/demos/latest';
      var pageFullPath = 'tutorials/GeneralizedKIC/generalized_kinematic_closure_1';
  </script>
  <script type="text/javascript" src="/demos/latest/javascript/jquery-1.7.2.min.js"></script>
  <script type="text/javascript" src="/demos/latest/javascript/mousetrap.min.js"></script>
  <script type="text/javascript" src="/demos/latest/javascript/gollum.js"></script>
  <script type="text/javascript" src="/demos/latest/javascript/gollum.dialog.js"></script>
  <script type="text/javascript" src="/demos/latest/javascript/gollum.placeholder.js"></script>
  <script type="text/javascript" src="/demos/latest/javascript/editor/gollum.editor.js"></script>
  <script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath:  [ ['\\(','\\)'] ],
      displayMath: [ ['$$','$$'], ['\\[','\\]'] ],
      processEscapes: true
    },
    TeX: { extensions: ["autoload-all.js"] }});
  </script>
  <script>(function(d,j){
  j = d.createElement('script');
  j.src = 'https://c328740.ssl.cf1.rackcdn.com/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML';
  (d.head || d.getElementsByTagName('head')[0]).appendChild(j);
  }(document));
  </script>
  

  <title>Generalized Kinematic Closure Tutorial 1:</title>
</head>
<body>

<div id="wiki-wrapper" class="page">
<div id="head">
  <h1>Generalized Kinematic Closure Tutorial 1:</h1>
  <ul class="actions">
    <li class="minibutton">
      <div id="searchbar">
        <form action="/demos/latest/search" method="get" id="search-form">
        <div id="searchbar-fauxtext">
          <input type="text" name="q" id="search-query" value="Search&hellip;" autocomplete="off">
          <a href="#" id="search-submit" title="Search this wiki">
            <span>Search</span>
          </a>
        </div>
        </form>
      </div>    </li>
    <li class="minibutton"><a href="/demos/latest/"
       class="action-home-page">Home</a></li>
    <li class="minibutton"><a href="https://rosettacommons.org/contact/"
       class="action-home-page">Feedback</a></li>
  </ul>
</div>
<div id="wiki-content">
<div class="">
  <div id="wiki-body" class="gollum-markdown-content">
    <div class="markdown-body">
      

<h1><a class="anchor" id="basic-loop-closure-with-generalizedkic" href="#basic-loop-closure-with-generalizedkic"><i class="fa fa-link"></i></a>Basic loop closure with GeneralizedKIC</h1>

<h1></h1>

<p>KEYWORDS: LOOPS SCRIPTING_INTERFACES</p>

<p>Tutorial by Vikram K. Mulligan (<a href="mailto:vmullig@uw.edu">vmullig@uw.edu</a>).  Created on 28 March 2017 for the Baker lab Rosetta Tutorial Series.  Updated 29 May 2017 for the new ref2015 default scorefunction.</p>

<p></p><div class="toc"><div class="toc-title">Table of Contents</div><ul><li><a href="#basic-loop-closure-with-generalizedkic">Basic loop closure with GeneralizedKIC</a><ul><li><a href="#basic-loop-closure-with-generalizedkic_goals">Goals</a></li><li><a href="#basic-loop-closure-with-generalizedkic_introduction-to-kinematic-closure-kic">Introduction to Kinematic Closure (KIC)</a></li><li><a href="#basic-loop-closure-with-generalizedkic_a-note-on-using-generalizedkic">A Note on Using GeneralizedKIC</a></li><li><a href="#basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts">Exercise 1: Building and Closing a Polypeptide Loop Using RosettaScripts</a><ul><li><a href="#basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_inputs">Inputs</a></li><li><a href="#basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_step-1-building-loop-geometry">Step 1: Building loop geometry</a></li><li><a href="#basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_step-2-preparing-for-sampling">Step 2: Preparing for sampling</a></li><li><a href="#basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_step-3-initial-generalizedkic-setup">Step 3: Initial GeneralizedKIC setup</a></li><li><a href="#basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_step-4-setting-loop-residues-and-picking-pivots">Step 4:  Setting loop residues and picking pivots</a></li><li><a href="#basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_step-5-setting-generalizedkic-perturbers">Step 5:  Setting GeneralizedKIC perturbers</a></li><li><a href="#basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_step-6-filtering-solutions-to-discard-bad-geometry">Step 6: Filtering solutions to discard bad geometry</a></li></ul></li><li><a href="#basic-loop-closure-with-generalizedkic_running-the-example-script">Running the example script</a></li><li><a href="#basic-loop-closure-with-generalizedkic_expected-output">Expected output</a></li><li><a href="#basic-loop-closure-with-generalizedkic_conclusion">Conclusion</a></li><li><a href="#basic-loop-closure-with-generalizedkic_further-reading">Further Reading</a></li></ul></li></ul></div>

<h2><a class="anchor" id="basic-loop-closure-with-generalizedkic_goals" href="#basic-loop-closure-with-generalizedkic_goals"><i class="fa fa-link"></i></a>Goals</h2>

<p>At the end of this tutorial, you will understand:</p>

<ul>
<li>What the kinematic closure algorithm is, and what problem it solves</li>
<li>How to use the PeptideStubMover to add loop residues to a pose lacking a loop</li>
<li>How to use the DeclareBond mover to create a bond</li>
<li>How to use the GeneralizedKIC mover to sample loop conformations</li>
<li>How to set up GeneralizedKIC perturbers, filters, and selectors</li>
<li>How to instruct GeneralizedKIC to close a peptide bond</li>
</ul>

<h2><a class="anchor" id="basic-loop-closure-with-generalizedkic_introduction-to-kinematic-closure-kic" href="#basic-loop-closure-with-generalizedkic_introduction-to-kinematic-closure-kic"><i class="fa fa-link"></i></a>Introduction to Kinematic Closure (KIC)</h2>

<p>Kinematic closure algorithms were originally developed for the robotics field to solve the problem of determining the necessary joint angles that would place a robot's hand or foot in a desired place.  We have adapted them for use within the Rosetta software suite to sample conformations of chains of atoms with well-defined start and end points.</p>

<p>A molecular kinematic closure problem may be described as follows: given a covalently-contiguous chain of atoms within a molecule, with covalent linkages at the ends of the chain fixing the start and end of the chain, what possible conformations maintain the integrity of bond length, bond angle, and dihedral angle restrictions within the chain?  To solve such a problem, we divide the chain of atoms into two segments, and define "pivot points" at the start of the chain (the first pivot), the end of the chain (the last pivot), and the breakpoint between the two segments (the middle pivot).</p>

<p>Having done this, the degrees of freedom within the two segments may be held fixed, randomized, perturbed, or otherwise altered as one sees fit.  These degrees of freedom include bond lengths, bond angles, and dihedral angles.  Whatever one does to these degrees of freedom, one ends up with two segments that still have well-defined rigid body transforms from the first pivot to the middle pivot (in the first segment), and from the middle pivot to the last pivot (in the second segment).  It is then possible to solve a system of equations for the six torsion angles adjacent to the three pivots in order to keep the system closed.  The matrix math that gives rise to the solution(s) is extremely fast as compared to alternative loop closure methods (which typically rely on iterative gradient-descent minimization); however, for a given system, this step may yield anywhere from 0 to 16 solutions.  It then becomes necessary to choose a solution for downstream molecular design or conformational refinement.</p>

<p>The GeneralizedKIC mover in Rosetta gives a user full control over pre-closure sampling, post-closure filtering, and selection of a closure solution.  It is fully accessible to the RosettaScripts scripting language, and interfaces nicely with other Rosetta movers and filters, allowing arbitrary protocols to be carried out on closure solutions before choosing a final solution.  It also allows closure of chains that do not consist solely of polypeptide backbones: that is, it is fully compatible with closure of atomic chains that run through disulfide bonds, arbitrary side-chain cross-links or cross-linkers, and non-canonical backbones.</p>

<p><strong>Overview of Kinematic Closure (KIC):</strong>
<img src="images/GenKIC_overview_sm.png" alt="Overview of Kinematic Closure (KIC)" /></p>

<h2><a class="anchor" id="basic-loop-closure-with-generalizedkic_a-note-on-using-generalizedkic" href="#basic-loop-closure-with-generalizedkic_a-note-on-using-generalizedkic"><i class="fa fa-link"></i></a>A Note on Using GeneralizedKIC</h2>

<p>A loop that is open may be thought of as a continuous loop containing a bond that is badly stretched, and which likely has very strange bond angles and torsion angles at the cutpoint.  GeneralizedKIC can close an open loop by using perturbations that set the bond length, bond angles, and, possibly, the torsion angle of the cutpoint to reasonable values prior to solving for pivot torsion values.</p>

<h2><a class="anchor" id="basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts" href="#basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts"><i class="fa fa-link"></i></a>Exercise 1: Building and Closing a Polypeptide Loop Using RosettaScripts</h2>

<h3><a class="anchor" id="basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_inputs" href="#basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_inputs"><i class="fa fa-link"></i></a>Inputs</h3>

<p>For this exercise, we will be using an NMR structure of an artificial mini-protein designed by Dr. Chris Bahl (PDB ID 2ND2).  This mini-protein is a 44-residue 3-helix bundle.  For the purposes of this tutorial, the structure has been stripped of its amino acid sequence (<em>i.e.</em> it has been mutated to poly-glycine), and the loop connecting the second and third helices has been deleted.  This is meant to simulate many common design cases, in which one might arrange secondary structure elements first and build loops later (<em>e.g.</em> in the case of parametric design approaches), as well as certain structure prediction cases, in which one might wish to model loops that are missing in crystal structures.  We will rebuild this loop and sample its possible conformations.</p>

<p><strong>The input structure, an edited version of PDB structure 2ND2 (<code>2ND2_state1_glyonly_loop_removed.pdb</code>):</strong>
<img src="images/Example1_input_structure.png" alt="The input structure" /></p>

<p>Additionally, we will use the following Rosetta flags file.  Briefly, this instructs Rosetta to run the input script 10 times to produce 10 sampled loop conformations, to use the <code>ref2015</code> score function, and to include all chemical bonds in the output PDB files (which can be convenient when debugging bad geometry, since bonds are drawn even if bonded atoms are too far apart).</p>

<p><strong>File <code>rosetta.flags</code>:</strong>
</p><pre class="highlight"><code>-nstruct 10
-in:file:s inputs/2ND2_state1_glyonly_loop_removed.pdb
-in:file:fullatom
-write_all_connect_info
-parser:protocol xml/exercise1.xml
-jd2:failed_job_exception false
-mute protocols.generalized_kinematic_closure.filter.GeneralizedKICfilter core.chemical.AtomICoor core.conformation.Residue</code></pre>

<h3><a class="anchor" id="basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_step-1-building-loop-geometry" href="#basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_step-1-building-loop-geometry"><i class="fa fa-link"></i></a>Step 1: Building loop geometry</h3>

<p>The GeneralizedKIC mover is only capable of sampling conformations of existing geometry.  It can neither add amino acid residues to a pose, nor create new bonds between residues.  For this reason, we must use the <a href="https://www.rosettacommons.org/docs/latest/PeptideStubMover">PeptideStubMover</a> to build the new loop, and the <a href="https://www.rosettacommons.org/docs/latest/scripting_documentation/RosettaScripts/Movers/movers_pages/DeclareBond">DeclareBond mover</a> to add a chemical bond across the loop cutpoint.</p>

<p>Run the <code>rosetta_scripts</code> application with no commandline options to create a template script, or copy and paste the example below:</p>

<pre class="highlight"><code><span class="nt">&lt;ROSETTASCRIPTS&gt;</span>
	<span class="nt">&lt;SCOREFXNS&gt;</span>
	<span class="nt">&lt;/SCOREFXNS&gt;</span>
	<span class="nt">&lt;RESIDUE_SELECTORS&gt;</span>
	<span class="nt">&lt;/RESIDUE_SELECTORS&gt;</span>
	<span class="nt">&lt;TASKOPERATIONS&gt;</span>
	<span class="nt">&lt;/TASKOPERATIONS&gt;</span>
	<span class="nt">&lt;FILTERS&gt;</span>
	<span class="nt">&lt;/FILTERS&gt;</span>
	<span class="nt">&lt;MOVERS&gt;</span>
	<span class="nt">&lt;/MOVERS&gt;</span>
	<span class="nt">&lt;APPLY_TO_POSE&gt;</span>
	<span class="nt">&lt;/APPLY_TO_POSE&gt;</span>
	<span class="nt">&lt;PROTOCOLS&gt;</span>
	<span class="nt">&lt;/PROTOCOLS&gt;</span>
	<span class="nt">&lt;OUTPUT</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;/ROSETTASCRIPTS&gt;</span></code></pre>

<p>Now let's add a <a href="https://www.rosettacommons.org/docs/latest/PeptideStubMover">PeptideStubMover</a> in the <code>&lt;MOVERS&gt;</code> section.  We will append three residues to the end of the second helix (residue 28), and prepend two residues to the start of the third helix (which was residue 29, but which becomes residue 32 after appending three residues).  Note that the <code>Insert</code> command is used instead of the <code>Append</code> command because the added residues are in the middle of the sequence.  We'll use a poly-alanine sequence for sampling, but will cheat a little bit just for the purposes of this tutorial by keeping a glycine at the second loop position, since this is present in the original structure.</p>

<pre class="highlight"><code><span class="nt">&lt;PeptideStubMover</span> <span class="na">name=</span><span class="s">"add_loop_residues"</span> <span class="nt">&gt;</span>
	<span class="nt">&lt;Insert</span> <span class="na">anchor_rsd=</span><span class="s">"28"</span> <span class="na">resname=</span><span class="s">"ALA"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;Insert</span> <span class="na">anchor_rsd=</span><span class="s">"29"</span> <span class="na">resname=</span><span class="s">"GLY"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;Insert</span> <span class="na">anchor_rsd=</span><span class="s">"30"</span> <span class="na">resname=</span><span class="s">"ALA"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;Prepend</span> <span class="na">anchor_rsd=</span><span class="s">"32"</span> <span class="na">resname=</span><span class="s">"ALA"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;Prepend</span> <span class="na">anchor_rsd=</span><span class="s">"32"</span> <span class="na">resname=</span><span class="s">"ALA"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;/PeptideStubMover&gt;</span>
</code></pre>

<p>Be sure to add the above mover to the <code>&lt;PROTOCOLS&gt;</code> section as well (<code>&lt;Add mover="add_loop_residues" /&gt;</code>).</p>

<p>We now have a five-residue loop, albeit one with several problems.  First, there is no bond between residues 30 and 31.  Second, these residues are too far apart in space to form a bond.  And third, all dihedral angles in the new loop are set to 0 degrees, including omega angles (<em>i.e.</em> all peptide bonds are <em>cis</em> instead of <em>trans</em>).  To solve the first problem, we will add a <a href="https://www.rosettacommons.org/docs/latest/scripting_documentation/RosettaScripts/Movers/movers_pages/DeclareBond">DeclareBond mover</a> to the <code>&lt;MOVERS&gt;</code> section of the script, telling Rosetta that there ought to be a chemical bond between the C atom of residue 30 and the N atom of residue 31.  Note that this does not move any geometry, but it does mean that the bond is present in the output PDB file if we run the script at this point.</p>

<pre class="highlight"><code><span class="nt">&lt;DeclareBond</span> <span class="na">name=</span><span class="s">"new_bond"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="na">res1=</span><span class="s">"31"</span> <span class="na">res2=</span><span class="s">"32"</span> <span class="nt">/&gt;</span></code></pre>

<p>As before, this must also be added to the <code>&lt;PROTOCOLS&gt;</code> section (<code>&lt;Add mover="new_bond" /&gt;</code>);</p>

<h3><a class="anchor" id="basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_step-2-preparing-for-sampling" href="#basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_step-2-preparing-for-sampling"><i class="fa fa-link"></i></a>Step 2: Preparing for sampling</h3>

<p>We will create a GeneralizedKIC mover for sampling in a moment.  Before we do so, though, we want to mutate two flanking residues, which will also be sampled as part of the loop, to alanine.  We do this because the sampling that we will use is biased by the Ramachandran preferences of the amino acid type.  Alanine is a good residue to use to represent the generic L-alpha amino acid, but glycine (which is currently present) is not because it has as much preference for the positive-phi region of Ramachandran space as for the negative.  (Indeed, our glycine Ramachandran tables are biased to <em>favour</em> the positive-phi region, since glycine is disproportionately found in the positive-phi region in the PDB structures used to train our scorefunction.)  Let us add two <a href="https://www.rosettacommons.org/docs/latest/scripting_documentation/RosettaScripts/Movers/movers_pages/MutateResidueMover">MutateResidue movers</a> to change the residue identities at this position.  In the <code>&lt;MOVERS&gt;</code> section add:</p>

<pre class="highlight"><code><span class="nt">&lt;MutateResidue</span> <span class="na">name=</span><span class="s">"mut1"</span> <span class="na">target=</span><span class="s">"28"</span> <span class="na">new_res=</span><span class="s">"ALA"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;MutateResidue</span> <span class="na">name=</span><span class="s">"mut2"</span> <span class="na">target=</span><span class="s">"34"</span> <span class="na">new_res=</span><span class="s">"ALA"</span> <span class="nt">/&gt;</span></code></pre>

<p>As before, add these two movers to the <code>&lt;PROTOCOLS&gt;</code> section after the movers already added.  At this point, the <code>&lt;PROTOCOLS&gt;</code> section should look like this:</p>

<pre class="highlight"><code><span class="nt">&lt;PROTOCOLS&gt;</span>
	<span class="nt">&lt;Add</span> <span class="na">mover=</span><span class="s">"add_loop_residues"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;Add</span> <span class="na">mover=</span><span class="s">"new_bond"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;Add</span> <span class="na">mover=</span><span class="s">"mut1"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;Add</span> <span class="na">mover=</span><span class="s">"mut2"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;/PROTOCOLS&gt;</span></code></pre>

<h3><a class="anchor" id="basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_step-3-initial-generalizedkic-setup" href="#basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_step-3-initial-generalizedkic-setup"><i class="fa fa-link"></i></a>Step 3: Initial GeneralizedKIC setup</h3>

<p>We're now ready to add the GeneralizedKIC mover that will close the gap in the loop and sample loop conformations.  In the movers section, add the following.</p>

<pre class="highlight"><code><span class="nt">&lt;GeneralizedKIC</span> <span class="na">name=</span><span class="s">"genkic"</span> <span class="nt">/&gt;</span></code></pre>

<p>Add this mover to the end of the <code>&lt;PROTOCOLS</code>&gt; section, too, as before.</p>

<p>GeneralizedKIC gives the user many, many options to control loop sampling, filtering, and solution selection.  Typically, the first option that one wants to set is the number of attempts that the mover will make to find a closed solution.  Each attempt consists of perturbing loop degrees of freedom (in a manner that we will define), solving for closed solutions, and applying GeneralizedKIC filters.  Because the KIC algorithm is so fast, one can easily attempt hundreds of solutions per second.  For our purposes, let's set the number of attempts to 5000 by modifying our GeneralizedKIC block as follows:</p>

<pre class="highlight"><code><span class="nt">&lt;GeneralizedKIC</span> <span class="na">name=</span><span class="s">"genkic"</span> <span class="na">closure_attempts=</span><span class="s">"5000"</span> <span class="nt">/&gt;</span></code></pre>

<p>Each attempt could yield anywhere from 0 to 16 solutions.  By default, every solution found will be stored until we've made the specified number of attempts (in our case 5000).  This could be far too many solutions, though.  It makes more sense to stop looking for solutions after we've found a small number.  That number could be as low as 1 (<em>i.e.</em> GeneralizedKIC stops as soon as a solution is found), but for our purposes, let's set that number at 5:</p>

<pre class="highlight"><code><span class="nt">&lt;GeneralizedKIC</span> <span class="na">name=</span><span class="s">"genkic"</span> <span class="na">closure_attempts=</span><span class="s">"5000"</span> <span class="na">stop_when_n_solutions_found=</span><span class="s">"5"</span> <span class="nt">/&gt;</span></code></pre>

<p>Even if we had set this numer at 1, a single attempt might have yielded up to 16 solutions.  We always need to tell GeneralizedKIC how to pick a single solution from among the solutions.  Here, we'll choose our solution by energy -- but there is an important caveat.  Since we are sampling backbone conformations, with no consideration of side-chains, we should use a scoring function that consists primarily of backbone-only terms to pick the best solution.  (Later we will see how we can apply an arbitrary mover -- <em>e.g.</em> a full repack and minimization -- to every solution, in which case it might make sense to use the full Rosetta scoring function to pick the best solution).  Let's set up a backbone-only scoring function using weights from the <code>ref2015</code> scoring function.  In the <code>&lt;SCOREFXNS&gt;</code> section of your script, add the following:</p>

<pre class="highlight"><code><span class="nt">&lt;ScoreFunction</span> <span class="na">name=</span><span class="s">"ref15sfxn"</span> <span class="na">weights=</span><span class="s">"ref2015.wts"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;ScoreFunction</span> <span class="na">name=</span><span class="s">"bb_only"</span> <span class="na">weights=</span><span class="s">"empty.wts"</span> <span class="nt">&gt;</span>
	<span class="nt">&lt;Reweight</span> <span class="na">scoretype=</span><span class="s">"fa_rep"</span> <span class="na">weight=</span><span class="s">"0.1"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;Reweight</span> <span class="na">scoretype=</span><span class="s">"fa_atr"</span> <span class="na">weight=</span><span class="s">"0.2"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;Reweight</span> <span class="na">scoretype=</span><span class="s">"hbond_sr_bb"</span> <span class="na">weight=</span><span class="s">"2.0"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;Reweight</span> <span class="na">scoretype=</span><span class="s">"hbond_lr_bb"</span> <span class="na">weight=</span><span class="s">"2.0"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;Reweight</span> <span class="na">scoretype=</span><span class="s">"rama_prepro"</span> <span class="na">weight=</span><span class="s">"0.45"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;Reweight</span> <span class="na">scoretype=</span><span class="s">"omega"</span> <span class="na">weight=</span><span class="s">"0.4"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;Reweight</span> <span class="na">scoretype=</span><span class="s">"p_aa_pp"</span> <span class="na">weight=</span><span class="s">"0.6"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;/ScoreFunction&gt;</span>
</code></pre>

<p>The "ref15sfxn" scoring function is now the full <code>ref2015</code> scoring function, which may be useful if we later add sidechain refinement to our protocol (which we will do in the third GeneralizedKIC tutorial).  For now, we will use the "bb_only" scoring function, in which we've cherry-picked relevant backbone terms (plus weakened versions of the Lennard-Jones terms).  Let's tell GeneralizedKIC to use this scoring function to pick a solution by adding two more options to our already-declared GeneralizedKIC mover:</p>

<pre class="highlight"><code><span class="nt">&lt;GeneralizedKIC</span> <span class="na">name=</span><span class="s">"genkic"</span> <span class="na">closure_attempts=</span><span class="s">"5000"</span> <span class="na">stop_when_n_solutions_found=</span><span class="s">"5"</span>
	<span class="na">selector=</span><span class="s">"lowest_energy_selector"</span> <span class="na">selector_scorefunction=</span><span class="s">"bb_only"</span>
<span class="nt">/&gt;</span></code></pre>

<h3><a class="anchor" id="basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_step-4-setting-loop-residues-and-picking-pivots" href="#basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_step-4-setting-loop-residues-and-picking-pivots"><i class="fa fa-link"></i></a>Step 4:  Setting loop residues and picking pivots</h3>

<p>It is now necessary to tell GeneralizedKIC which residues are in the loop to be closed, and to give it the pivot points to use.  You will recall that pivots define the two segments into which we are dividing the loop to be closed.  They do <em>not</em> need to correspond to discontinuities in the loop, but they do need freely rotatable bonds adjacent to them (making N and C atoms, which are adjacent to a peptide bond with a fixed dihedral value, unsuitable for use as pivots).  The KIC solver will assign solution values to the torsions adjacent to the pivots, which is why free rotation is necessary for these torsions.  The following additions to our GeneralizedKIC mover define a loop running from residue 28 through 34, and set the alpha carbons of residues 28, 31, and 34 as pivot atoms:</p>

<pre class="highlight"><code><span class="nt">&lt;GeneralizedKIC</span> <span class="err">...</span> <span class="nt">&gt;</span>
	<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"28"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"29"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"30"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"31"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"32"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"33"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"34"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;SetPivots</span> <span class="na">res1=</span><span class="s">"28"</span> <span class="na">res2=</span><span class="s">"31"</span> <span class="na">res3=</span><span class="s">"34"</span> <span class="na">atom1=</span><span class="s">"CA"</span> <span class="na">atom2=</span><span class="s">"CA"</span> <span class="na">atom3=</span><span class="s">"CA"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;/GeneralizedKIC&gt;</span></code></pre>

<p>The ellipsis above represents the options that we have already set.  Note that first and last pivot atoms must be at the start and end of the loop to be sampled.  Shifting these pivots inward prevents sampling of degrees of freedom beyond the pivots (which, as we will see in Tutorial 4, is occasionally the behaviour that one desires).</p>

<h3><a class="anchor" id="basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_step-5-setting-generalizedkic-perturbers" href="#basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_step-5-setting-generalizedkic-perturbers"><i class="fa fa-link"></i></a>Step 5:  Setting GeneralizedKIC perturbers</h3>

<p>Perturbers allow a user to alter degrees of freedom in the two segments between the pivots.  They can:</p>

<ul>
<li>Set a degree of freedom to a fixed value</li>
<li>Perturb a degree of freedom slighly from a starting value (<em>i.e.</em> add a small, random value to the value of the degree of freedom)</li>
<li>Fully randomize a degree of freedom</li>
<li>Draw a random value for a degree of freedom from a biased distribution (<em>e.g.</em> drawing mainchain torsion values from the Ramachandran distribution for the relevant amino acid type)</li>
</ul>

<p>Perturbers are applied in the order in which they are defined, and can override or modify the effect of previous perturbers.  One could, for example, set a particular torsion value to 180, then allow small perturbations around that value, through successive application of a setting and a perturbing perturber.</p>

<p>We want to use perturbers to do several things:
1.  Set all mainchain omega values to 180 degrees.
2.  Set the bond length, bond angles, and torsion angle of the currently-broken bond between residues 30 and 31 to ideal values for a peptide bond.
3.  Randomize phi and psi values for all amino acids in the loop, biased by each amino acid's Ramachandran map.</p>

<p>Within the <code>&lt;GeneralizedKIC&gt; ... &lt;/GeneralizedKIC&gt;</code> block, we can add a <code>set_dihedral</code> perturber to set the values of mainchain omega angles.  We use <code>&lt;AddAtoms&gt;</code> tags to define each omega angle that we're setting, and an <code>&lt;AddValue&gt;</code> tag to define the value to which we're setting them.  (Note that the same value is applied to all of these in this example.  We could also add one <code>&lt;AddValue&gt;</code> tag for each <code>&lt;AddAtoms&gt;</code> tag if we wanted to set all of them to different values.)</p>

<pre class="highlight"><code><span class="nt">&lt;GeneralizedKIC</span> <span class="err">...</span><span class="nt">&gt;</span>
	...
	<span class="nt">&lt;AddPerturber</span> <span class="na">effect=</span><span class="s">"set_dihedral"</span> <span class="nt">&gt;</span>
		<span class="nt">&lt;AddAtoms</span> <span class="na">res1=</span><span class="s">"28"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">res2=</span><span class="s">"29"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddAtoms</span> <span class="na">res1=</span><span class="s">"29"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">res2=</span><span class="s">"30"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddAtoms</span> <span class="na">res1=</span><span class="s">"30"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">res2=</span><span class="s">"31"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddAtoms</span> <span class="na">res1=</span><span class="s">"31"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">res2=</span><span class="s">"32"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddAtoms</span> <span class="na">res1=</span><span class="s">"32"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">res2=</span><span class="s">"33"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddAtoms</span> <span class="na">res1=</span><span class="s">"33"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">res2=</span><span class="s">"34"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddValue</span> <span class="na">value=</span><span class="s">"180.0"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;/AddPerturber&gt;</span>
<span class="nt">&lt;/GeneralizedKIC&gt;</span></code></pre>

<p>We could similarly use a <code>set_bondlength</code> perturber, two <code>set_bondangle</code> perturbers, and a <code>set_dihedral</code> perturber to set ideal peptide bond geometry for the bond between residues 30 and 31.  However, GeneralizedKIC provides a convenient shorthand for combining these perturbers:</p>

<pre class="highlight"><code><span class="nt">&lt;GeneralizedKIC</span> <span class="err">...</span><span class="nt">&gt;</span>
	...
	<span class="nt">&lt;CloseBond</span> <span class="na">res1=</span><span class="s">"31"</span> <span class="na">res2=</span><span class="s">"32"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="na">bondlength=</span><span class="s">"1.328685"</span> <span class="na">angle1=</span><span class="s">"121.699997"</span> <span class="na">angle2=</span><span class="s">"116.199993"</span> <span class="na">torsion=</span><span class="s">"180.0"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;/GeneralizedKIC&gt;</span></code></pre>

<p>Finally, the <code>randomize_backbone_by_rama_prepro</code> perturber can be used for biased randomization of mainchain torsions of any residue that (a) has a Ramachandran map in the Rosetta database, and (b) has all of its mainchain torsions within the chain to be sampled by GeneralizedKIC.  (That is, we cannot use it for, for example, a cysteine residue involved in a disulfide bond if we are closing through the disulfide bond.)</p>

<pre class="highlight"><code><span class="nt">&lt;GeneralizedKIC</span> <span class="err">...</span><span class="nt">&gt;</span>
	...
	<span class="nt">&lt;AddPerturber</span> <span class="na">effect=</span><span class="s">"randomize_backbone_by_rama_prepro"</span> <span class="nt">&gt;</span>
		<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"28"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"29"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"30"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"31"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"32"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"33"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"34"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;/AddPerturber&gt;</span>
<span class="nt">&lt;GeneralizedKIC&gt;</span></code></pre>

<p>At this point, your GeneralizedKIC mover should look like this:</p>

<pre class="highlight"><code><span class="nt">&lt;GeneralizedKIC</span> <span class="na">name=</span><span class="s">"genkic"</span>	<span class="na">closure_attempts=</span><span class="s">"5000"</span> <span class="na">stop_when_n_solutions_found=</span><span class="s">"5"</span>
	<span class="na">selector=</span><span class="s">"lowest_energy_selector"</span> <span class="na">selector_scorefunction=</span><span class="s">"bb_only"</span>
<span class="nt">&gt;</span>
	<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"28"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"29"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"30"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"31"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"32"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"33"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"34"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;SetPivots</span> <span class="na">res1=</span><span class="s">"28"</span> <span class="na">res2=</span><span class="s">"31"</span> <span class="na">res3=</span><span class="s">"34"</span> <span class="na">atom1=</span><span class="s">"CA"</span> <span class="na">atom2=</span><span class="s">"CA"</span> <span class="na">atom3=</span><span class="s">"CA"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;AddPerturber</span> <span class="na">effect=</span><span class="s">"set_dihedral"</span> <span class="nt">&gt;</span>
		<span class="nt">&lt;AddAtoms</span> <span class="na">res1=</span><span class="s">"28"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">res2=</span><span class="s">"29"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddAtoms</span> <span class="na">res1=</span><span class="s">"29"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">res2=</span><span class="s">"30"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddAtoms</span> <span class="na">res1=</span><span class="s">"30"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">res2=</span><span class="s">"31"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddAtoms</span> <span class="na">res1=</span><span class="s">"31"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">res2=</span><span class="s">"32"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddAtoms</span> <span class="na">res1=</span><span class="s">"32"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">res2=</span><span class="s">"33"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddAtoms</span> <span class="na">res1=</span><span class="s">"33"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">res2=</span><span class="s">"34"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddValue</span> <span class="na">value=</span><span class="s">"180.0"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;/AddPerturber&gt;</span>
	<span class="nt">&lt;CloseBond</span> <span class="na">res1=</span><span class="s">"31"</span> <span class="na">res2=</span><span class="s">"32"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="na">bondlength=</span><span class="s">"1.328685"</span> <span class="na">angle1=</span><span class="s">"121.699997"</span> <span class="na">angle2=</span><span class="s">"116.199993"</span> <span class="na">torsion=</span><span class="s">"180.0"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;AddPerturber</span> <span class="na">effect=</span><span class="s">"randomize_backbone_by_rama_prepro"</span> <span class="nt">&gt;</span>
		<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"28"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"29"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"30"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"31"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"32"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"33"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"34"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;/AddPerturber&gt;</span>
<span class="nt">&lt;/GeneralizedKIC&gt;</span></code></pre>

<h3><a class="anchor" id="basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_step-6-filtering-solutions-to-discard-bad-geometry" href="#basic-loop-closure-with-generalizedkic_exercise-1-building-and-closing-a-polypeptide-loop-using-rosettascripts_step-6-filtering-solutions-to-discard-bad-geometry"><i class="fa fa-link"></i></a>Step 6: Filtering solutions to discard bad geometry</h3>

<p>If you run the script at this point, it should produce closed loop solutions.  There are a number of possible problems with the solutions produced, however.  First, although the residues within each segment are being sampled in a biased manner based on their respective Ramachandran maps, the pivot residues have values assigned to them by the solver, which may put them in awkward regions of Ramachandran space.  We want to filter out solutions with poor pivot Ramachandran energies.  Second, we don't want loop solutions with clashing geometry, so we want some sort of bump check to be applied before accepting a solution.  And third, we may want to impose some prior knowledge insofar as we expect the first and last residues of the loop, which are coming off of helices, to be in the alpha-helical bin ("A") of Ramachandran space.</p>

<p>GeneralizedKIC filters are applied rapidly to all solutions produced by the KIC solver <em>before</em> the solutions are used to build computationally-expensive Pose geometry.  They are therefore a good way to cheaply and efficiently discard bad solutions.  Note that, unlike Rosetta's filters, the GeneralizedKIC filters operate on a set of loop degree-of-freedom values, not on a full Pose.</p>

<p>Let us first require that solutions have residues 28 ad 34 in the alpha-helical region of Ramachandran space.  For this, we use a <code>backbone_bin</code> GeneralizedKIC filter:</p>

<pre class="highlight"><code><span class="nt">&lt;GeneralizedKIC</span> <span class="err">...</span><span class="nt">&gt;</span>
	...
	<span class="nt">&lt;AddFilter</span> <span class="na">type=</span><span class="s">"backbone_bin"</span> <span class="na">residue=</span><span class="s">"28"</span> <span class="na">bin_params_file=</span><span class="s">"ABBA"</span> <span class="na">bin=</span><span class="s">"A"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;AddFilter</span> <span class="na">type=</span><span class="s">"backbone_bin"</span> <span class="na">residue=</span><span class="s">"34"</span> <span class="na">bin_params_file=</span><span class="s">"ABBA"</span> <span class="na">bin=</span><span class="s">"A"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;/GeneralizedKIC&gt;</span></code></pre>

<p>In the above, the "ABBA" bin parameters file, located in the Rosetta database, defines Ramachandran bins for the alpha-helical region ("A"), the beta-sheet region ("B"), and the mirror-image regions that can be accessed by D-amino acids ("Aprime" and "Bprime", respectively).</p>

<p>Next, we'll add a simple bump check filter (<code>loop_bump_check</code>) to discard solutions with clashing mainchain geometry.  Note that this does <em>not</em> check sidechain geometry; it only operates on the heavyatoms of the loop to be closed:</p>

<pre class="highlight"><code><span class="nt">&lt;GeneralizedKIC</span> <span class="err">...</span><span class="nt">&gt;</span>
	...
	<span class="nt">&lt;AddFilter</span> <span class="na">type=</span><span class="s">"loop_bump_check"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;/GeneralizedKIC&gt;</span></code></pre>

<p>And finally, we'll add a <code>rama_prepro_check</code> filter to discard solutions in which pivot atoms are in energetically-unfavourable regions of Ramachandran space:</p>

<pre class="highlight"><code><span class="nt">&lt;AddFilter</span> <span class="na">type=</span><span class="s">"rama_prepro_check"</span> <span class="na">residue=</span><span class="s">"28"</span> <span class="na">rama_cutoff_energy=</span><span class="s">"0.5"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;AddFilter</span> <span class="na">type=</span><span class="s">"rama_prepro_check"</span> <span class="na">residue=</span><span class="s">"31"</span> <span class="na">rama_cutoff_energy=</span><span class="s">"0.5"</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;AddFilter</span> <span class="na">type=</span><span class="s">"rama_prepro_check"</span> <span class="na">residue=</span><span class="s">"34"</span> <span class="na">rama_cutoff_energy=</span><span class="s">"0.5"</span> <span class="nt">/&gt;</span></code></pre>

<p>And that's it!  The finished script should look like this:</p>

<pre class="highlight"><code><span class="nt">&lt;ROSETTASCRIPTS&gt;</span>
	<span class="nt">&lt;SCOREFXNS&gt;</span>
		<span class="nt">&lt;ScoreFunction</span> <span class="na">name=</span><span class="s">"ref15sfxn"</span> <span class="na">weights=</span><span class="s">"ref2015.wts"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;ScoreFunction</span> <span class="na">name=</span><span class="s">"bb_only"</span> <span class="na">weights=</span><span class="s">"empty.wts"</span> <span class="nt">&gt;</span>
			<span class="nt">&lt;Reweight</span> <span class="na">scoretype=</span><span class="s">"fa_rep"</span> <span class="na">weight=</span><span class="s">"0.1"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;Reweight</span> <span class="na">scoretype=</span><span class="s">"fa_atr"</span> <span class="na">weight=</span><span class="s">"0.2"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;Reweight</span> <span class="na">scoretype=</span><span class="s">"hbond_sr_bb"</span> <span class="na">weight=</span><span class="s">"2.0"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;Reweight</span> <span class="na">scoretype=</span><span class="s">"hbond_lr_bb"</span> <span class="na">weight=</span><span class="s">"2.0"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;Reweight</span> <span class="na">scoretype=</span><span class="s">"rama_prepro"</span> <span class="na">weight=</span><span class="s">"0.45"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;Reweight</span> <span class="na">scoretype=</span><span class="s">"omega"</span> <span class="na">weight=</span><span class="s">"0.4"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;Reweight</span> <span class="na">scoretype=</span><span class="s">"p_aa_pp"</span> <span class="na">weight=</span><span class="s">"0.6"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;/ScoreFunction&gt;</span>
	<span class="nt">&lt;/SCOREFXNS&gt;</span>
	<span class="nt">&lt;RESIDUE_SELECTORS&gt;</span>
	<span class="nt">&lt;/RESIDUE_SELECTORS&gt;</span>
	<span class="nt">&lt;TASKOPERATIONS&gt;</span>
	<span class="nt">&lt;/TASKOPERATIONS&gt;</span>
	<span class="nt">&lt;FILTERS&gt;</span>
	<span class="nt">&lt;/FILTERS&gt;</span>
	<span class="nt">&lt;MOVERS&gt;</span>	
		<span class="nt">&lt;PeptideStubMover</span> <span class="na">name=</span><span class="s">"add_loop_residues"</span> <span class="nt">&gt;</span>
			<span class="nt">&lt;Insert</span> <span class="na">anchor_rsd=</span><span class="s">"28"</span> <span class="na">resname=</span><span class="s">"ALA"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;Insert</span> <span class="na">anchor_rsd=</span><span class="s">"29"</span> <span class="na">resname=</span><span class="s">"GLY"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;Insert</span> <span class="na">anchor_rsd=</span><span class="s">"30"</span> <span class="na">resname=</span><span class="s">"ALA"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;Prepend</span> <span class="na">anchor_rsd=</span><span class="s">"32"</span> <span class="na">resname=</span><span class="s">"ALA"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;Prepend</span> <span class="na">anchor_rsd=</span><span class="s">"32"</span> <span class="na">resname=</span><span class="s">"ALA"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;/PeptideStubMover&gt;</span>
	
		<span class="nt">&lt;DeclareBond</span> <span class="na">name=</span><span class="s">"new_bond"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="na">res1=</span><span class="s">"31"</span> <span class="na">res2=</span><span class="s">"32"</span> <span class="nt">/&gt;</span>

		<span class="nt">&lt;MutateResidue</span> <span class="na">name=</span><span class="s">"mut1"</span> <span class="na">target=</span><span class="s">"28"</span> <span class="na">new_res=</span><span class="s">"ALA"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;MutateResidue</span> <span class="na">name=</span><span class="s">"mut2"</span> <span class="na">target=</span><span class="s">"34"</span> <span class="na">new_res=</span><span class="s">"ALA"</span> <span class="nt">/&gt;</span>

		<span class="nt">&lt;GeneralizedKIC</span> <span class="na">name=</span><span class="s">"genkic"</span> <span class="na">selector=</span><span class="s">"lowest_energy_selector"</span> <span class="na">selector_scorefunction=</span><span class="s">"bb_only"</span>
			<span class="na">closure_attempts=</span><span class="s">"5000"</span> <span class="na">stop_when_n_solutions_found=</span><span class="s">"5"</span> <span class="nt">&gt;</span>
			<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"28"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"29"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"30"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"31"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"32"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"33"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;AddResidue</span> <span class="na">res_index=</span><span class="s">"34"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;SetPivots</span> <span class="na">res1=</span><span class="s">"28"</span> <span class="na">res2=</span><span class="s">"31"</span> <span class="na">res3=</span><span class="s">"34"</span> <span class="na">atom1=</span><span class="s">"CA"</span> <span class="na">atom2=</span><span class="s">"CA"</span> <span class="na">atom3=</span><span class="s">"CA"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;AddPerturber</span> <span class="na">effect=</span><span class="s">"set_dihedral"</span> <span class="nt">&gt;</span>
				<span class="nt">&lt;AddAtoms</span> <span class="na">res1=</span><span class="s">"28"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">res2=</span><span class="s">"29"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="nt">/&gt;</span>
				<span class="nt">&lt;AddAtoms</span> <span class="na">res1=</span><span class="s">"29"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">res2=</span><span class="s">"30"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="nt">/&gt;</span>
				<span class="nt">&lt;AddAtoms</span> <span class="na">res1=</span><span class="s">"30"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">res2=</span><span class="s">"31"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="nt">/&gt;</span>
				<span class="nt">&lt;AddAtoms</span> <span class="na">res1=</span><span class="s">"31"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">res2=</span><span class="s">"32"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="nt">/&gt;</span>
				<span class="nt">&lt;AddAtoms</span> <span class="na">res1=</span><span class="s">"32"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">res2=</span><span class="s">"33"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="nt">/&gt;</span>
				<span class="nt">&lt;AddAtoms</span> <span class="na">res1=</span><span class="s">"33"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">res2=</span><span class="s">"34"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="nt">/&gt;</span>
				<span class="nt">&lt;AddValue</span> <span class="na">value=</span><span class="s">"180.0"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;/AddPerturber&gt;</span>
			<span class="nt">&lt;CloseBond</span> <span class="na">res1=</span><span class="s">"31"</span> <span class="na">res2=</span><span class="s">"32"</span> <span class="na">atom1=</span><span class="s">"C"</span> <span class="na">atom2=</span><span class="s">"N"</span> <span class="na">bondlength=</span><span class="s">"1.328685"</span> <span class="na">angle1=</span><span class="s">"121.699997"</span> <span class="na">angle2=</span><span class="s">"116.199993"</span> <span class="na">torsion=</span><span class="s">"180.0"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;AddPerturber</span> <span class="na">effect=</span><span class="s">"randomize_backbone_by_rama_prepro"</span> <span class="nt">&gt;</span>
				<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"28"</span> <span class="nt">/&gt;</span>
				<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"29"</span> <span class="nt">/&gt;</span>
				<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"30"</span> <span class="nt">/&gt;</span>
				<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"31"</span> <span class="nt">/&gt;</span>
				<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"32"</span> <span class="nt">/&gt;</span>
				<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"33"</span> <span class="nt">/&gt;</span>
				<span class="nt">&lt;AddResidue</span> <span class="na">index=</span><span class="s">"34"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;/AddPerturber&gt;</span>
			<span class="nt">&lt;AddFilter</span> <span class="na">type=</span><span class="s">"backbone_bin"</span> <span class="na">residue=</span><span class="s">"28"</span> <span class="na">bin_params_file=</span><span class="s">"ABBA"</span> <span class="na">bin=</span><span class="s">"A"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;AddFilter</span> <span class="na">type=</span><span class="s">"backbone_bin"</span> <span class="na">residue=</span><span class="s">"34"</span> <span class="na">bin_params_file=</span><span class="s">"ABBA"</span> <span class="na">bin=</span><span class="s">"A"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;AddFilter</span> <span class="na">type=</span><span class="s">"loop_bump_check"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;AddFilter</span> <span class="na">type=</span><span class="s">"rama_prepro_check"</span> <span class="na">residue=</span><span class="s">"28"</span> <span class="na">rama_cutoff_energy=</span><span class="s">"0.5"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;AddFilter</span> <span class="na">type=</span><span class="s">"rama_prepro_check"</span> <span class="na">residue=</span><span class="s">"31"</span> <span class="na">rama_cutoff_energy=</span><span class="s">"0.5"</span> <span class="nt">/&gt;</span>
			<span class="nt">&lt;AddFilter</span> <span class="na">type=</span><span class="s">"rama_prepro_check"</span> <span class="na">residue=</span><span class="s">"34"</span> <span class="na">rama_cutoff_energy=</span><span class="s">"0.5"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;/GeneralizedKIC&gt;</span>
	
	<span class="nt">&lt;/MOVERS&gt;</span>
	<span class="nt">&lt;APPLY_TO_POSE&gt;</span>
	<span class="nt">&lt;/APPLY_TO_POSE&gt;</span>
	<span class="nt">&lt;PROTOCOLS&gt;</span>
		<span class="nt">&lt;Add</span> <span class="na">mover=</span><span class="s">"add_loop_residues"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;Add</span> <span class="na">mover=</span><span class="s">"new_bond"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;Add</span> <span class="na">mover=</span><span class="s">"mut1"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;Add</span> <span class="na">mover=</span><span class="s">"mut2"</span> <span class="nt">/&gt;</span>
		<span class="nt">&lt;Add</span> <span class="na">mover=</span><span class="s">"genkic"</span> <span class="nt">/&gt;</span>
	<span class="nt">&lt;/PROTOCOLS&gt;</span>
	<span class="nt">&lt;OUTPUT</span> <span class="nt">/&gt;</span>
<span class="nt">&lt;/ROSETTASCRIPTS&gt;</span></code></pre>

<h2><a class="anchor" id="basic-loop-closure-with-generalizedkic_running-the-example-script" href="#basic-loop-closure-with-generalizedkic_running-the-example-script"><i class="fa fa-link"></i></a>Running the example script</h2>

<p>The above script is provided in the <code>demos/tutorials/GeneralizedKIC/exercise1/xml/</code> directory.  To run this, navigate to the <code>demos/tutorials/GeneralizedKIC</code> directory and type the following:</p>

<pre class="highlight"><code><span class="nv">$&gt;</span> <span class="nb">cd </span>exercise1
<span class="nv">$&gt;</span> <span class="nv">$ROSETTA3</span>/bin/rosetta_scripts.default.linuxgccrelease @inputs/rosetta.flags
<span class="nv">$&gt;</span> <span class="nb">cd</span> ..</code></pre>

<p>In the above, <code>$ROSETTA3</code> is the path to your Rosetta directory.  You may need to replace <code>linuxgccrelease</code> for your operating system and compilation (<em>e.g.</em> <code>macosclangrelease</code> on a Mac).</p>

<h2><a class="anchor" id="basic-loop-closure-with-generalizedkic_expected-output" href="#basic-loop-closure-with-generalizedkic_expected-output"><i class="fa fa-link"></i></a>Expected output</h2>

<p>When tested with Rosetta 3.8 SHA 3cad483ccac973741499159e12989a7143bf79de (nightly build from Tuesday, March 28th, 2017), the script produced many loop conformations, including some closely resembling the native conformation:</p>

<p><strong>A solution closely matching the native conformation (cyan -- native, orange -- GeneralizedKIC solution)</strong>
<img src="images/Example1_top_solution.png" alt="A solution closely matching the native conformation" /></p>

<p><strong>A solution more distinct from the native conformation (cyan -- native, orange -- GeneralizedKIC solution)</strong>
<img src="images/Example1_not_quite_right_solution.png" alt="A solution more distinct from the native conformation" /></p>

<h2><a class="anchor" id="basic-loop-closure-with-generalizedkic_conclusion" href="#basic-loop-closure-with-generalizedkic_conclusion"><i class="fa fa-link"></i></a>Conclusion</h2>

<p>In this tutorial, we have covered basic loop building and closure with GeneralizedKIC.  The use of perturbers for sampling and filters for pruning solutions was also covered.  The reader would be well-advised to play with the various settings, and to explore the different GeneralizedKIC perturbers, filters, and selectors that are available, all of which are documented in detail in the <a href="https://www.rosettacommons.org/docs/latest/scripting_documentation/RosettaScripts/composite_protocols/generalized_kic/GeneralizedKIC">GeneralizedKIC documentation</a> pages on the Rosetta help wiki.</p>

<h2><a class="anchor" id="basic-loop-closure-with-generalizedkic_further-reading" href="#basic-loop-closure-with-generalizedkic_further-reading"><i class="fa fa-link"></i></a>Further Reading</h2>

<p>Bhardwaj G, Mulligan VK, Bahl CD, Gilmore JM, Harvey PJ, Cheneval O, Buchko GW, Pulavarti SV, Kaas Q, Eletsky A, Huang PS, Johnsen WA, Greisen PJ, Rocklin GJ, Song Y, Linsky TW, Watkins A, Rettie SA, Xu X, Carter LP, Bonneau R, Olson JM, Coutsias E, Correnti CE, Szyperski T, Craik DJ, Baker D.  (2016).  Accurate de novo design of hyperstable constrained peptides.  <em>Nature</em> 538(7625):329-335.</p>

<p>Mandell DJ, Coutsias EA, Kortemme T. (2009).  Sub-angstrom accuracy in protein loop reconstruction by robotics-inspired conformational sampling.  <em>Nat. Methods</em> 6(8):551-2.</p>

<p>Coutsias EA, Seok C, Jacobson MP, Dill KA.  (2004).  A kinematic view of loop closure.  <em>J. Comput. Chem.</em> 25(4):510-28.</p>

<p><a href="https://www.rosettacommons.org/docs/latest/scripting_documentation/RosettaScripts/composite_protocols/generalized_kic/GeneralizedKIC">GeneralizedKIC documentation</a></p>

<p><a class="internal present" href="/demos/latest/tutorials/GeneralizedKIC/generalized_kinematic_closure_2">GeneralizedKIC Tutorial 2</a></p>

<p><a class="internal present" href="/demos/latest/tutorials/GeneralizedKIC/generalized_kinematic_closure_3">GeneralizedKIC Tutorial 3</a></p>

<p><a class="internal present" href="/demos/latest/tutorials/GeneralizedKIC/generalized_kinematic_closure_4">GeneralizedKIC Tutorial 4</a></p>

    </div>
  </div>
  </div>

</div>
</div>

<form name="rename" method="POST" action="/demos/latest/rename/tutorials/GeneralizedKIC/generalized_kinematic_closure_1">
  <input type="hidden" name="rename"/>
  <input type="hidden" name="message"/>
</form>


</body>
</html>
