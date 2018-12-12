// steps 
1- Vaut mieux commencer par créer header.php, index.php, style.css, et functions.php, sidebar.php si on en a besoin



/****** To start with header.php *******/

<!DOCTYPE html>
<html lang="fr">
<head>
	<title>
		<?php bloginfo('name') ?>
		<?php if ( is_404() ) : ?> &raquo; 
		<?php _e('Not Found') ?>
			<?php elseif ( is_home() ) : ?> &raquo; 
				<?php bloginfo('description') ?>
			<?php else : ?>
				<?php wp_title() ?>
			<?php endif ?>
	</title>
 
	<meta http-equiv="Content-Type" content="<?php bloginfo('html_type'); ?>; charset=<?php bloginfo('charset'); ?>" />
	<meta name="generator" content="WordPress <?php bloginfo('version'); ?>" />
	<link rel="stylesheet" href="<?php bloginfo('stylesheet_url'); ?>" type="text/css" media="screen" />
	<?php wp_get_archives('type=monthly&format=link'); ?>
	<?php //comments_popup_script(); // off by default ?>
	<?php wp_head(); ?>
 
</head>
<body>
	<div id="page">
		<div id="header">
			<h1><a href="<?php bloginfo('url'); ?>"><?php bloginfo('name'); ?></a></h1>
			<?php bloginfo('description'); ?>
		</div>
    
    
/***** Then index.php *******/

<?php get_header(); ?>

	<div id="content">
		<?php if(have_posts()) : ?>
			<?php while(have_posts()) : the_post(); ?>
				<div class="post" id="post-<?php the_ID(); ?>">
					<div class="imageList">
						<?php
							if (has_post_thumbnail()) {
								the_post_thumbnail('thumbnail');
							}
						?>
					</div>
					<a href="<?php the_permalink(); ?>" title="Lire article"><?php the_title('<h2>','</h2>'); ?></a>
					<!-- postmetada-->
					<p class="postmetadata">
						Par: <?php the_author(); ?> | Le <?php the_time('j F Y'); ?> | Dans: <?php the_category(', '); ?>
						| <?php comments_popup_link(); ?>
					</p>
					<?php the_excerpt(); ?>
				</div>
			<?php endwhile; ?>
		<?php endif; ?>
	</div>
	<?php
		get_sidebar();
	?>

	<?php
		get_footer();
		wp_footer(); 
	?> 
</div><!--Fin de id_page-->

</body>
</html>
	
/***** Then style.css ****/

*{box-sizing: border-box;}

#page {
	width: 90%;
	margin: 15px auto;
	border: 1px solid black;
	border-radius: 3px;
	padding: 2px;
	overflow: hidden;
}

#content {
	width: 75%;
	float: left;
}

#header {
	background: url(img/header.jpg);
	color: red;
}

.sidebar {
	width: 20%;
	float: right;
}
.sidebar li {
	list-style-type: none;
}


#footer {
	color: black;
	clear: both;
	padding: 2em 1%;
	overflow: hidden;
}

.widgetFooter {
	border: 1px solid black;
	border-radius: 3px;
	padding: 2px;
	width: 31.5%;
	float: left;
	margin: 0.5%;
}

.tac {
	text-align: center;
}

.stopclear {
	clear: both;
}

.imageList {
	display: inline;
	float: left;
}



/***** functions.php *****/
Avec des le depert add_theme_support('post-thumbnails'); 

/***** The sidebar *****/
sidebar.php
<div class="sidebar">
	<?php dynamic_sidebar('l1'); ?> 
</div>

avec functions.php + d'autres widgets pour le footer

<?php
if ( function_exists('register_sidebar') )
	$args = array(
		'name' => 'Barre laterale',
		'id' => 'l1',
		'description' => 'Zone laterale gauche des pages'
	);
register_sidebar($args);

$args = array(
		'name' => 'Footer Gauche',
		'id' => 'g1',
		'description' => 'Footer gauche',
		'before_widget' => '<div class="widgetFooter">',
		'after_widget' => '</div>',
	);
register_sidebar($args);

//creation de la zone de widget footer droit
$args = array(
		'name' => 'Footer droit',
		'id' => 'z1',
		'description' => 'Footer droit',
		'before_widget' => '<div class="widgetFooter">',
		'after_widget' => '</div>',
	);
register_sidebar($args);

//creation de la zone de widget footer centre
<?php
if ( function_exists('register_sidebar') )
	$args = array(
		'name' => 'Barre laterale',
		'id' => 'l1',
		'description' => 'Zone laterale gauche des pages'
	);
register_sidebar($args);

$args = array(
		'name' => 'Footer Gauche',
		'id' => 'g1',
		'description' => 'Footer gauche',
		'before_widget' => '<div class="widgetFooter">',
		'after_widget' => '</div>',
	);
register_sidebar($args);

//creation de la zone de widget footer droit
$args = array(
		'name' => 'Footer droit',
		'id' => 'z1',
		'description' => 'Footer droit',
		'before_widget' => '<div class="widgetFooter">',
		'after_widget' => '</div>',
	);
register_sidebar($args);

//creation de la zone de widget footer centre
$args = array(
		'name' => 'Footer centre',
		'id' => 'k1',
		'description' => 'Footer centre',
		'before_widget' => '<div class="widgetFooter">',
		'after_widget' => '</div>',
	);
register_sidebar($args);

add_theme_support('post-thumbnails'); 

 ?>
 
/******* 404.php *******/
 <?php get_header(); ?>

<div id="content">
	<h2>Oupsss  Page non trouvable</h2>
	<div id="moteur">

	</div>
</div>
<?php
	get_sidebar();
?>

<?php
	get_footer();
	wp_footer(); 
?> 
</div><!--Fin de id_page-->

</body>
</html>
 
 
